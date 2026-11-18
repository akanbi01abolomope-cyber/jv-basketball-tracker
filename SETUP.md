# JV Basketball Coach Tracker — Cloud Sync Setup

This package keeps the existing tracker and adds Firebase Authentication + Cloud Firestore live sync.

## Important
- Do not publish Firestore rules that allow everyone to read/write. This tracker can contain student information.
- Replace the two example email addresses in `firestore.rules` with the exact email addresses for the two authorized accounts.
- The app uses one shared team document. Signed-in authorized users see the same roster and practice data.
- Local browser storage remains as a local copy/backup. Export a JSON backup before enabling cloud sync.
- Firebase configuration values in the web app are project identifiers, not admin credentials. Never put a service-account private key in this app.

## 1. Create a Firebase project
1. Open https://console.firebase.google.com/ and create a project.
2. Add a Web app to the project. Register it with any nickname, such as `JV Coach Tracker`.
3. Copy the Firebase web configuration values.
4. In `index.html`, find `const FIREBASE_CONFIG = { ... }` and replace `PASTE_API_KEY_HERE`, `PASTE_PROJECT_ID_HERE`, and `PASTE_APP_ID_HERE` with the matching values from Firebase. Keep `authDomain` as `<your-project-id>.firebaseapp.com`.

## 2. Enable sign-in
1. In Firebase Console, open **Authentication → Get started → Sign-in method**.
2. Enable **Email/Password**.
3. Open **Authentication → Users → Add user**.
4. Create one account for yourself and one for your coach. Use separate passwords and share each person's login only with that person.

## 3. Create the database
1. Open **Firestore Database → Create database**.
2. Choose production mode and a region appropriate for your school/team.
3. Open the **Rules** tab.
4. Replace the rules with the contents of `firestore.rules` after changing the two example email addresses to the exact account emails.
5. Publish the rules.

## 4. Deploy the updated app
1. Upload the contents of this folder to the root of your existing GitHub Pages repository, replacing the old `index.html`, `manifest.webmanifest`, and `sw.js` and adding `firestore.rules`, `SETUP.md`, and the icons folder.
2. Commit the changes and wait for GitHub Pages to publish.
3. Open the app URL, sign in, and check that the cloud status says live sync is on.
4. Sign in on your coach's phone using the coach's account. Changes should appear on both devices.

## 5. First sync behavior
- If the shared Firestore team document does not exist yet, the first authorized account to sign in uploads that browser's current tracker data.
- If it already exists, the cloud copy becomes the shared copy on sign-in.
- Export a backup from the device with the correct/current roster before the first sign-in.

## Notes
- Keep Firebase Authentication and Firestore enabled for the project.
- Firestore has usage quotas and billing settings; check the Firebase console for current limits.
- The app currently syncs the full team data document. Avoid simultaneous edits to the same field at the exact same time; the most recent save can replace the earlier version.
- The app's web hosting and Firebase database are separate services. Updating GitHub Pages publishes app code; Firebase stores team data.
