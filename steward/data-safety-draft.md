# Data Safety Form — DRAFT (manual review required)

> **Status:** DRAFT. The Play Console Data Safety form is binding once
> submitted. Re-read every answer below against the live app before clicking
> **Submit** in Play Console. If a future release adds analytics, ads, cloud
> sync, or any networked data movement, the answers below MUST be revised.

These answers reflect the app as of `versionCode 9` / `version 0.2.7`, which:

- stores all financial data in a local SQLite database on the device,
- has no user account, login, or backend,
- uses `expo-updates` to fetch JS bundle updates from Expo's update server,
- uses `expo-secure-store` for an optional local PIN,
- schedules **local** notifications (not push) for loan reminders.

---

## Section: Data collection and security

**Does your app collect or share any of the required user data types?**
**Answer:** **No.**

Reasoning:
- "Collect" in Google's definition means data that is transmitted off the
  device. The app does not transmit any user-entered data off the device.
- The Expo OTA update request is technical metadata about the app build, not
  user data. It does not include any of the data categories Google enumerates
  in this form.

If Play Console rejects "No" because of the OTA update traffic, switch to:

> **Yes**, then declare:
> - Data type: **App activity → Other app activity** (or **App info and
>   performance → Crash logs**, whichever Google's reviewer requests).
> - Purpose: **App functionality** (specifically, app updates).
> - Collected: **No** (data is processed transiently and not retained for the
>   developer's purposes).
> - Shared with third parties: **No**.
> - Required: **No** (treated as optional from the user's perspective; OTA
>   can be disabled by removing the `updates` block in `app.json`).

**Is all of the user data collected by your app encrypted in transit?**
**Answer:** **Yes** (Expo's OTA endpoint uses HTTPS).

**Do you provide a way for users to request that their data be deleted?**
**Answer:** **Yes — data is stored only on the user's device.** Users can
delete data per-entry inside the app, or remove all data by clearing the
app's storage or uninstalling the app. There is no remote copy to delete.

---

## Section: Data types — itemized

For each row below, the recommended Play Console answer is **Not collected**,
because none of these categories are transmitted off the device.

| Category                                | Collected? | Reason |
| --------------------------------------- | ---------- | ------ |
| Personal info (name, email, address, ID numbers, etc.) | **No** | Never transmitted. Names you type for accounts, categories, or "person owed" stay on-device. |
| Financial info (transactions, payment info, credit info, other) | **No** | All entries stay on-device. The app does not process real payments. |
| Health and fitness                      | **No** | N/A |
| Messages (emails, SMS, in-app messages) | **No** | N/A |
| Photos and videos                       | **No** | N/A |
| Audio files                             | **No** | N/A |
| Files and docs                          | **No** | N/A |
| Calendar                                | **No** | N/A |
| Contacts                                | **No** | N/A |
| App activity (interactions, search history, installed apps, other) | **No** | No analytics SDK is wired up. |
| Web browsing                            | **No** | N/A |
| App info and performance (crash logs, diagnostics, other) | **No** | No crash reporter is wired up. Play vitals only. |
| Device or other IDs                     | **No** | The app does not read advertising ID, IMEI, or similar. |
| Location (approximate, precise)         | **No** | The app never asks for location permission. |
| Audio (voice, sound recordings)         | **No** | N/A |

If at any point you add Sentry, Firebase Analytics, Crashlytics, or any
similar SDK, you MUST come back and update this section.

---

## Section: Security practices

- **Data encrypted in transit:** **Yes** (HTTPS for OTA).
- **Users can request data be deleted:** **Yes** — local-only storage,
  user-controlled.
- **Committed to Play Families Policy:** Not applicable; not targeting
  children.
- **Independent security review:** **No.**

---

## Section: Permissions used by the app

These are not part of Data Safety per se, but Play Console will surface them.
Confirm before launch.

- `POST_NOTIFICATIONS` (Android 13+): used to display **local** loan due-date
  reminders. Optional; the app continues to work if denied.
- Internet: used by `expo-updates` to check for OTA updates. Standard for any
  Expo-based release.

The app does **not** request: location, camera, microphone, contacts,
calendar, storage / media library, SMS, phone, biometrics, or background
location.
