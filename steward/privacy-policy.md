# Privacy Policy — Steward (my KapayamanFi)

**Last updated:** 2026-04-27

This privacy policy describes how the Android application **Steward** (package
name `com.melvs.mykapayamanfi`, hereafter "the app") handles information. The
app is a personal finance tracker built and maintained by an individual
developer ("we", "us") and is distributed through the Google Play Store.

> Before publishing, replace the contact email below and host this document at
> a stable public URL. Google Play requires the privacy policy URL to be
> reachable without login.

## Summary

- The app stores all of your financial data **locally on your device**.
- The app does **not** create an account, does **not** sign you in, and does
  **not** sync your data to any server.
- The app does **not** sell or share your personal or financial data with
  third parties.
- The only outbound network traffic is the standard Expo over-the-air update
  check (see "Network Activity" below).

## Information We Process

### Information you enter
You can enter the following inside the app:

- Account names (e.g. "Cash", "GCash", "BPI") and optional notes.
- Opening balances and credit-card-related fields (statement day, monthly
  budget, payment due window).
- Income and expense entries: amount, account, category, date, and optional
  notes.
- Loans you record (borrowed or lent): the other person's name, amount,
  optional interest rate, term, due date, status, and notes.
- Loan payments and account-to-account transfers.
- Custom income / expense category names.
- App preferences (e.g. currency).
- An optional numeric PIN to lock the app.

All of this data is stored in a local SQLite database on your device. It is
not transmitted off the device by the app.

### Information automatically collected
The app does not include any analytics SDK, advertising SDK, or crash reporting
SDK. We do not collect device identifiers, IP addresses, location, contacts,
photos, or any other content from your device.

### Notifications
If you grant notification permission, the app schedules **local** notifications
on your device to remind you of upcoming loan due dates. These notifications
are generated and delivered locally by Android. No server is involved and no
data leaves your device for this feature.

### Secure storage
If you enable the optional PIN lock, the PIN is stored using Android's secure
storage (via `expo-secure-store`). It is not transmitted off the device.

## Network Activity

The app uses Expo's over-the-air update mechanism (`expo-updates`). When the
app starts it may make a request to Expo's update server
(`https://u.expo.dev/...`) to check whether a new JavaScript bundle is
available, and may download that bundle. This request includes basic technical
metadata required by the update protocol (such as the runtime version of the
app). It does not include the contents of your accounts, entries, loans, or
any other financial data.

The app does not make any other network calls in normal operation.

## How We Use Your Information

Information you enter is used solely to:

- display your accounts, balances, entries, loans, and totals inside the app,
- compute derived values (e.g. account balances, loan progress),
- schedule local reminder notifications you opted into.

We do not use your information for advertising, profiling, or analytics.

## Sharing

We do not share, sell, rent, or trade your information with third parties.
There is no backend operated by us. Because the data lives on your device, the
people who can see it are the people who can unlock your phone (and unlock the
app's PIN, if you set one).

## Your Choices and Controls

- **Edit or delete entries.** You can edit or delete any account, entry, loan,
  payment, transfer, or category from inside the app at any time.
- **Notifications.** You can revoke notification permission at any time in
  Android system settings; the app will simply stop scheduling reminders.
- **Delete all data.** Uninstalling the app, or clearing its storage from
  Android settings, removes the local database and any stored PIN.

Because the data is local, we cannot delete it for you remotely.

## Data Retention

Your data remains on your device until you delete it or uninstall the app.

## Children's Privacy

The app is not directed to children under 13. It is a personal finance utility
intended for general personal use.

## Security

Your data is stored in your device's app-private storage. The optional PIN is
stored using Android's secure storage. The security of your device — screen
lock, OS updates, full-disk encryption — is your responsibility.

## Changes to This Policy

We may update this policy as the app changes. The "Last updated" date at the
top will reflect the most recent revision. If a future version of the app adds
features that change the information handling described here (for example,
optional cloud backup), the policy will be updated before that release.

## Contact

For questions about this policy, contact:

> **Email:** melvsmmelo@gmail.com

If a different developer or business name is used on the Play Console listing,
update this section to match that name.
