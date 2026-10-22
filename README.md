# Robotics Inventory: setup on GitHub Pages (free)

GitHub Pages only hosts web pages. It cannot store data. So this app keeps its data in
**Firebase** (Google's free "Spark" plan, no credit card needed). The setup is about 15 minutes.

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com and click **Create a project** (turn Analytics off).
2. In the project, click the **</>** (Web) icon and register an app. Copy the `firebaseConfig` values.
3. Open `index.html` and paste `apiKey`, `authDomain`, `projectId` and `appId` into `FIREBASE_CONFIG` at the top.
   Also put your own Google email in `ADMIN_EMAILS`. (The apiKey is not a secret; the rules in step 3 protect your data.)

## 2. Turn on sign-in
**Build → Authentication → Get started → Sign-in method → Google → Enable → Save.**

## 3. Create the database and rules
1. **Build → Firestore Database → Create database** (choose any location, start in *production mode*).
2. Open the **Rules** tab, paste the contents of `firestore.rules`, and edit the email lists:
   - `isAdmin`: your email (you can add, edit and import items).
   - `isStaff`: your colleagues' Google emails (they can sign items in and out).
3. Click **Publish**.

## 4. Put it on GitHub Pages
1. Create a GitHub repository and upload `index.html` to it.
2. **Settings → Pages → Deploy from a branch → main → / (root) → Save.**
3. After a minute your link appears: `https://YOUR-USERNAME.github.io/REPO-NAME/`
4. Back in Firebase: **Authentication → Settings → Authorized domains → Add domain** and add `YOUR-USERNAME.github.io`.
   (Without this, Google sign-in will fail.)

## 5. Load your inventory
Open your link, sign in, go to **Manage → Import list**, and paste the rows from `inventory-import.csv`
(you can leave out the first header line).

## Notes
- Anyone not listed in `firestore.rules` can sign in but sees "No access" and no data.
- To add a colleague later, add their email to `isStaff` in the Rules tab and click Publish.
- Don't paste real passwords or other secrets into the page; everything in `index.html` is public on GitHub.
