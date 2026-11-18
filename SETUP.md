# JV Basketball Coach Tracker — Firebase sync setup

The app is pre-filled with the Firebase web configuration for project `jv-basketball-tracker`. It still needs Firebase Authentication and Firestore enabled and authorized email addresses added to the security rules.

## 1. Enable sign-in
1. Firebase Console → Authentication → Get started.
2. Sign-in method → enable **Email/Password**.
3. Authentication → Users → Add user. Create a separate account for the coach and another for the app administrator. Do not share passwords.

## 2. Create Firestore
1. Firebase Console → Firestore Database → Create database.
2. Choose **Production mode** and a region appropriate for your team.
3. Open the **Rules** tab. In `firestore.rules`, replace `YOUR_EMAIL@example.com` and `COACH_EMAIL@example.com` with the exact sign-in email addresses for the two authorized accounts.
4. Paste the edited rules into the Rules tab and click **Publish**. Do not use public read/write rules.

## 3. Deploy to GitHub Pages
Replace the existing app files with the contents of this folder (keep `index.html` at the repository root), commit, and wait for GitHub Pages to publish.

## 4. First sync
Before signing in, export a JSON backup from the device that has the correct/current roster and practice data. The first authorized sign-in creates the shared team document using that device's data. Later sign-ins load the shared cloud copy.

## 5. Coach access
Give the coach their own Firebase Authentication account. Add their exact email to the Firestore rules allowlist. They open the same GitHub Pages URL and sign in. Changes should sync live between signed-in devices.

## Privacy and data handling
This tracker may contain student information. Get the coach/school's approval before storing it in a cloud service, use only authorized accounts, and avoid adding sensitive notes. The Firebase web config is client-side project configuration, not an admin credential; never publish service-account private keys.
