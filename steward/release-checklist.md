# Play Console Release Checklist — Steward (my KapayamanFi)

This file lists everything that still needs a human in the loop to publish the
app to Google Play. Items marked **[manual]** can only be done from the Play
Console or from your own machine — they cannot be automated from the codebase.

Current build metadata (from `app.json` / `package.json`):

- App display name: **Steward**
- Package: `com.melvs.mykapayamanfi`
- `expo.version`: `0.2.7`
- `android.versionCode`: `9`
- EAS project ID: `abfc4fc4-cbbd-4bc0-bb9d-cdb12b4ddb4d`

## 0. Pre-publish sanity

- [ ] Run `npm run typecheck` and confirm clean.
- [ ] Launch on a real Android device (not just emulator) and walk through:
      add account → add income → add expense → add loan → record loan payment
      → transfer between accounts → mark a credit-card cycle paid → set/remove
      a PIN → grant notifications and confirm a reminder fires for a near-due
      loan.
- [ ] Confirm fresh-install seeding works (default Cash account, default
      categories, currency = PHP).

## 1. Build

- [ ] **[manual]** Produce a signed AAB for the production track:
      `eas build --profile production --platform android`
- [ ] **[manual]** Download the resulting `.aab` from Expo / EAS.
- [ ] Bump `expo.version` and `android.versionCode` in `app.json` for any
      subsequent release. Play Console rejects re-uploads with the same
      `versionCode`.

## 2. Play Console — App content

- [ ] **[manual]** Privacy Policy URL: host `privacy-policy.md` (rendered as
      HTML or Markdown) at a stable public URL and paste it into
      *App content → Privacy policy*. Replace the placeholder support email
      in the policy first.
- [ ] **[manual]** App access: the app has no login. Select "All functionality
      is available without restrictions."
- [ ] **[manual]** Ads: select "No, my app does not contain ads."
- [ ] **[manual]** Content rating questionnaire: complete it. The app has no
      user-generated content that is shared, no chat, no gambling, no violence.
- [ ] **[manual]** Target audience and content: target audience is adults
      (18+). The app is not directed at children.
- [ ] **[manual]** News app declaration: No.
- [ ] **[manual]** COVID-19 contact tracing & status: No.
- [ ] **[manual]** Data safety form: see `data-safety-draft.md`. Mark draft
      as reviewed and submit.
- [ ] **[manual]** Government apps: No.
- [ ] **[manual]** Financial features declaration (Personal Loan / etc.):
      The app does **not** issue, broker, or facilitate loans, and does not
      handle real money movement. It is a personal record-keeping utility.
      Decline all financial-features categories.

## 3. Play Console — Store listing

- [ ] **[manual]** App name: `Steward` (must match `expo.name`).
- [ ] **[manual]** Short description: paste from
      `play-store-short-description.md`.
- [ ] **[manual]** Full description: paste from
      `play-store-full-description.md`.
- [ ] **[manual]** App icon (512x512 PNG): export from
      `assets/icon.png` if needed; Play requires a separate hi-res icon
      asset.
- [ ] **[manual]** Feature graphic (1024x500 PNG): not in repo yet — create
      one before publishing.
- [ ] **[manual]** Phone screenshots: minimum 2, recommended 4–8. Capture
      from a real device or emulator. Suggested screens: Dashboard, Accounts
      list, Add expense form, Loans list, Loan detail.
- [ ] **[manual]** App category: `Finance`.
- [ ] **[manual]** Tags: choose `Personal finance` if available.
- [ ] **[manual]** Contact details: support email, optional website / phone.

## 4. Play Console — Pricing & distribution

- [ ] **[manual]** Choose countries. (Recommended: at minimum Philippines.)
- [ ] **[manual]** Pricing: Free.
- [ ] **[manual]** Device categories: Phone (and Tablet if desired). Wear OS,
      TV, Auto: not supported.

## 5. Releases

- [ ] **[manual]** Recommended path for first launch: upload the AAB to
      *Internal testing* first, install via the tester link, smoke-test on
      Melvs's own phone.
- [ ] **[manual]** Promote to *Closed testing* (or *Production*) once
      confident.
- [ ] **[manual]** Release notes ("What's new in this release"): keep them
      short. Suggested first release note:
      "Initial release: track cash accounts, income, expenses, loans, and
      transfers offline."

## 6. After publish

- [ ] **[manual]** Verify the listing on a clean Google account; install via
      Play and confirm the app boots, seeds defaults, and runs offline.
- [ ] **[manual]** Confirm the privacy policy URL still resolves once the
      listing is live (Play scans periodically and will warn if it 404s).
- [ ] **[manual]** Watch the *Pre-launch report* in Play Console for
      crashes / ANRs on the device matrix Google runs the build on.

## 7. Known follow-ups not blocking launch

- The app uses `expo-updates` (OTA) pointing at `u.expo.dev`. This is
  disclosed in the privacy policy. If you decide to disable OTA before
  launch, remove the `updates` block from `app.json` and remove the matching
  paragraph from `privacy-policy.md`.
- There is no in-app backup / export. Document this clearly in the listing
  (already mentioned in the full description). Consider adding export to
  CSV / JSON before a wider rollout.
- No crash reporting is wired up; you will only see crashes via Play
  Console's Android vitals.

## 8. Repo housekeeping

- [ ] **[manual]** `git fetch` / `git pull origin main` before starting a
      release. (The automation pass that produced this checklist could not
      complete `git pull` because non-interactive HTTPS auth to GitHub was
      not available; pull manually.)
- [ ] **[manual]** Tag the release commit, e.g. `git tag v0.2.7 && git push
      --tags`, after the AAB is uploaded.
