---
name: firebase-push-notifications
description: Firebase Cloud Messaging (FCM) push notifications for web and Android — topics, quotas, setup, and the Spark-plan limits. Use when an app needs to notify users of something urgent, like an emergency blood request.
---

# Firebase Cloud Messaging (FCM)

## What it is

Firebase Cloud Messaging is Google's free push-notification service for
Android, iOS and web. A server (or the Firebase console) sends a message;
FCM delivers it to the user's device even when the app is closed. The
headline use case that drove this skill: emergency blood-request alerts —
when someone posts an urgent request for A+ in Dhaka, nearby A+ donors get
a phone notification instantly instead of having to open the app and check.

## When to use

- Emergency alerts to a matching group of users (the headline use case).
- "Someone replied to your request", new nearby listing, app update
  available.
- **Not** for in-app chat, email, or anything needing guaranteed delivery
  receipts — FCM is push transport only; it has no inbox, no delivery log
  UI, and no retry guarantees beyond best-effort.

## Cost / limits (verified from Firebase docs, Nov 2026)

- **Cost: no-cost on both Spark and Blaze** — no per-message charge, no
  monthly cap (Firebase pricing page).
- **600,000 messages/minute per project** (default quota; covers >99% of
  developers per Firebase). 429 `QUOTA_EXCEEDED` if exceeded — retry with
  exponential backoff, minimum 1-minute initial delay.
- **Per Android device:** max 240 messages/minute, 5,000/hour.
- **Payload:** max 4,096 bytes total; **topic messages max 2,048 bytes**.
- **Batch send:** up to 500 messages per Admin SDK `sendEach` / `sendAll`
  call.
- **Topics:** unlimited topics, unlimited subscribers per topic; one app
  instance can subscribe to max 2,000 topics; 3,000 topic-subscription
  changes/second per project. A topic send counts against the quota **per
  subscriber** (1M subscribers = 1M messages).
- Device groups are **deprecated** and stop working 29 Sep 2027 — do not
  build on them; use topics or stored tokens.

## How it works (concepts)

- **Registration token:** each app install gets a unique token. Store it
  in Firestore (e.g. `users/{uid}/fcmTokens`), keyed to whatever the
  targeting needs (blood group + district, for example), and delete it
  when FCM reports it invalid.
- **Topics:** devices subscribe to a topic string; one send reaches all
  subscribers. Ideal pattern for the blood app: `blood_Apos_Dhaka`,
  `blood_Opos_Chattogram`, `emergency_all`. No token storage needed for
  topic sends.
- **Notification vs data messages:**
  - *Notification message* — FCM displays it automatically (title/body).
    Simple, works even if the app is killed.
  - *Data message* — silent payload your app code handles (e.g. refresh
    the request list, play a custom sound). Use when the app must act,
    not just display.
  - A message can carry both.
- **Sending routes:** (a) Firebase console → Cloud Messaging composer —
  manual, no code, good for one-off announcements; (b) Admin SDK / HTTP
  v1 API from a trusted server — needed for automatic sends (e.g. "new
  emergency request → notify matching donors").

## Setup — Web app

Web push **requires a service worker** and a **VAPID key**; without the
worker, background notifications never arrive.

1. Firebase console → Project settings → Cloud Messaging → **Web Push
   certificates** → Generate key pair (VAPID key). Keep it in the web
   config.
2. Create `firebase-messaging-sw.js` in the public/site root (must be
   served from the site root):

   ```js
   importScripts('https://www.gstatic.com/firebasejs/10.13.2/firebase-app-compat.js');
   importScripts('https://www.gstatic.com/firebasejs/10.13.2/firebase-messaging-compat.js');
   firebase.initializeApp({ apiKey: '...', authDomain: '...', projectId: '...',
     messagingSenderId: '...', appId: '...' });
   const messaging = firebase.messaging();
   messaging.onBackgroundMessage((payload) => { /* optional custom handling */ });
   ```

3. In app code, ask permission and get the token, then save it to
   Firestore:

   ```js
   import { getMessaging, getToken, onMessage } from 'firebase/messaging';
   const messaging = getMessaging(app);
   const permission = await Notification.requestPermission(); // must be 'granted'
   const token = await getToken(messaging, { vapidKey: 'YOUR_VAPID_KEY' });
   // save token + targeting fields to Firestore
   onMessage(messaging, (payload) => { /* foreground: show in-app banner/toast */ });
   ```

4. **Gotcha:** `Notification.requestPermission()` must be called from a
   user gesture in some browsers; if the user denies, there is no
   re-prompt until they change site settings. Explain *why* before asking
   ("Allow notifications so urgent blood requests reach you").
5. **Gotcha:** web push works in Chrome/Edge/Firefox on desktop and
   Android Chrome; **iOS Safari web push only works for sites added to the
   Home Screen (iOS 16.4+)** and is unreliable — treat Android app/web-on-
   Android as the reliable path.

## Setup — Android app (APK)

1. Add Firebase to the Android project (google-services.json).
2. Add the Messaging SDK dependency and, on **Android 13+ (API 33+)**,
   request the `POST_NOTIFICATIONS` runtime permission — without it,
   notifications are silently dropped even though FCM delivers them.
3. Android delivery **requires Google Play Services** on the device. Most
   Bangladeshi Android phones have it; Huawei phones without GMS will not
   receive FCM.
4. Get the token in the app (`FirebaseMessaging.getInstance().token`) and
   upload it to Firestore with the targeting fields; subscribe to topics,
   e.g. `FirebaseMessaging.getInstance().subscribeToTopic("blood_Apos_Dhaka")`.
5. Handle foreground messages (`onMessageReceived` in a
   `FirebaseMessagingService`) and background messages (FCM shows
   notification messages automatically).

## Sending — automatic emergency alerts (the real use case)

Flow: user posts emergency request → a trusted sender notifies matching
donors.

```js
// Server-side (Admin SDK, Node.js) — send to a topic, no token list needed
const { getMessaging } = require('firebase-admin/messaging');
await getMessaging().send({
  topic: 'blood_Apos_Dhaka',
  notification: { title: 'জরুরি রক্ত দরকার: A+ (ঢাকা)',
                  body: 'ঢাকা মেডিকেলে A+ রক্ত দরকার — এখনই দেখুন' },
  data: { requestId: 'abc123', bloodGroup: 'A+', district: 'Dhaka' },
  android: { priority: 'high', notification: { channelId: 'emergency', sound: 'default' } },
});
```

- **Targeting by blood group + district = topics** (`blood_Apos_Dhaka`). A
  donor subscribes on registration and unsubscribes if their
  group/district changes.
- Keep the payload tiny (topic cap 2,048 bytes): title, body, requestId
  only — the app fetches full details from Firestore on open.

## Gotchas

- **Spark plan blocks the automatic path:** Cloud Functions (the natural
  trigger: "on new emergency request → send FCM") requires the **Blaze**
  plan. On Spark, options are: (a) manual sends from the console composer
  (free, works today — admin pastes the alert), (b) a small external
  server running the Admin SDK, or (c) upgrade to Blaze (pay-as-you-go;
  FCM itself stays free, Functions has a 2M invocations/month no-cost
  tier). Do **not** put the service-account key in the web app — sending
  must happen from a trusted environment only.
- **Anonymous Auth + tokens:** apps using Anonymous Auth have the FCM
  token as the only link to a device. If the user clears app data /
  reinstalls, the token changes — refresh it on every app start and prune
  invalid tokens on send errors
  (`messaging/registration-token-not-registered`).
- **Delivery is best-effort, not guaranteed:** do not promise "every donor
  will be notified". Battery optimisation / Doze can delay messages; use
  `priority: 'high'` for emergency alerts (Android) and keep the message
  short.
- **High-priority abuse risk:** only emergency requests should be high
  priority; routine messages sent high-priority can get throttled by the
  system.
- **Web vs APK:** the hosted web app can do push on Android Chrome, but
  installed APK push is more reliable (no browser permission quirks,
  works when the browser is closed). For emergency alerts, prioritise the
  APK path.
- **Token storage privacy:** FCM tokens are device identifiers — store
  them in Firestore under the user's own record with rules that only that
  user (and the admin sender) can read them; never publish them.

## Sources

- Pricing (FCM: no-cost on Spark & Blaze): https://firebase.google.com/pricing
- Pricing plans (Cloud Functions needs Blaze): https://firebase.google.com/docs/projects/billing/firebase-pricing-plans
- Receive messages in web apps (service worker): https://firebase.google.com/docs/cloud-messaging/web/receive-messages
- Throttling and quotas (600k/min, per-device limits, payload sizes): https://firebase.google.com/docs/cloud-messaging/throttling-and-quotas
- FCM overview / send from Admin SDK: https://firebase.google.com/docs/cloud-messaging
