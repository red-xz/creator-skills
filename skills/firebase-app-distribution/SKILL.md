---
name: firebase-app-distribution
description: Distribute pre-release Android builds to invited testers by email, without the Play Store. Use when sharing a new APK build with specific people before or instead of a Play Store release.
---

# Firebase App Distribution

## What it is

Firebase App Distribution distributes pre-release Android (and iOS) builds
to invited testers without the Play Store. You upload an APK or AAB, invite
testers by email, and they install it from the Firebase **App Tester** app
on their phone. It replaces expiring one-off download links with a permanent
tester channel where every new build appears automatically.

## When to use

- Sharing a new APK build with testers (yourself, family, staff) before /
  instead of Play Store release.
- Any time a build needs to reach specific people by email, with release
  notes and version history, instead of a public link anyone can open.
- **Not** for public distribution to all users — testers must be invited
  by email and sign in with a Google account.

## Cost / limits (verified from Firebase docs, Nov 2026)

- **Cost: no-cost** on both Spark and Blaze plans (Firebase pricing page
  lists App Distribution as free).
- **500 testers per Firebase project**; **200 testers per group**. A
  no-cost limit increase can be requested.
- **1,000 releases per app** (oldest releases auto-removed past the cap).
- **Releases expire after 150 days**; a notice appears 30 days before
  expiry.
- **Tester invitations expire after 30 days** if not accepted.
- Max binary size reported as 2048 MiB (~2 GB) in community guides — not
  confirmed on an official page; small APKs (~4 MB) are far below any
  plausible cap.

## Prerequisites

1. Firebase project exists.
2. Android app registered in the project (add Firebase to the Android
   project — at minimum create the project and register the app;
   `google-services.json` needed only if the app itself uses other
   Firebase products).
3. Firebase CLI installed and signed in (`firebase login`).
4. A **signed** APK (debug key or app signing key) or AAB built in
   Android Studio.
5. **AAB only:** the Firebase Android app must be linked to a Google Play
   developer account (Firebase console → Project settings → Integrations
   → Google Play → Link). APKs do **not** need this — prefer APK if you
   have no Play Console account yet.

## Setup — one-time (console)

1. Firebase console → **App Distribution** → select project → select app
   → **Get started**.
2. Create a tester group (e.g. `beta-testers`) and add tester emails, or
   add testers per release.
3. Testers: open the email invitation on their Android phone → sign in
   with the invited Google account → install the **App Tester** app from
   Play Store → the build appears there → tap Install.

## Distribute a build — CLI (recommended, scriptable)

```bash
# APK
firebase appdistribution:distribute my-app-v7.apk \
  --app 1:PROJECT_NUMBER:android:APP_ID \
  --release-notes "v7: emergency request fixes" \
  --testers "user@example.com,tester2@example.com"
# or a whole group, and/or a testers file (one email per line):
firebase appdistribution:distribute app.apk --app <APP_ID> \
  --groups "beta-testers" --testers-file testers.txt
```

- Find the App ID in Firebase console → Project settings → General
  (looks like `1:1234567890:android:0a1b2c3d4e5f67890`).
- The CLI prints a release link after upload; it can be shared with
  testers who already have access.
- AAB variant: same command with an `.aab` file (requires the Play link
  above; Google Play's internal app sharing processes it into
  device-optimised APKs).

## Distribute a build — console (no CLI)

Firebase console → App Distribution → Releases → select app → drag the
APK in → pick tester groups/individuals → add release notes →
**Distribute**. Testers get an email automatically.

## Manage testers

```bash
firebase appdistribution:testers:add tester@example.com --project <PROJECT_ID>
firebase appdistribution:testers:remove tester@example.com --project <PROJECT_ID>
```

Groups are managed in the console (App Distribution → Testers & Groups).

## Gotchas

- **Testers need a Google account** matching the invited email, and must
  accept within 30 days. This is **not** a public download link: random
  users cannot install from it.
- **It does not replace the Play Store** for the general public. It is a
  tester channel; the 150-day expiry means old builds vanish —
  re-distribute if a tester is still on an old build months later.
- **Spark plan is fine** — no Blaze upgrade needed, no billing.
- **AAB + Play link caveat:** until a Play Console account exists ($25,
  card + ID verification), distribute **APKs**, which need no Play link.
- The APK must be **signed** — the Android Studio "Generate Signed App
  Bundle / APK" output already is; an unsigned debug APK from a raw build
  may be rejected.
- Firebase CLI auth: the CLI's stored token can expire (~1h). If
  `appdistribution:distribute` fails with 401, refresh the token before
  retrying.
- Do **not** put the service-account key or tester emails into a public
  repo; keep `testers.txt` in a private deploy folder, which is never
  pushed to GitHub.

## Sources

- Distribute APK via CLI: https://firebase.google.com/docs/app-distribution/android/distribute-cli?apptype=apk
- Distribute via console: https://firebase.google.com/docs/app-distribution/android/distribute-console
- AAB via CLI (Play link required): https://firebase.google.com/docs/app-distribution/android/distribute-cli?apptype=aab
- Add/remove testers + limits: https://firebase.google.com/docs/app-distribution/add-remove-search-testers
- Troubleshooting & FAQ (limits, expiry): https://firebase.google.com/docs/app-distribution/troubleshooting
- Pricing (App Distribution: no-cost): https://firebase.google.com/pricing
