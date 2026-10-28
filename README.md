# Allowance for Mama & Papa

A phone-friendly tracker for the weekly allowance the family gives to Mama and Papa. It shows the next collection date, who paid, the amount, status, and an 8-week chart. The data lives in Firebase (free Spark plan), and the page is hosted free on GitHub Pages. Changes show up live on everyone's phone.

## 1. Set the database rules

1. Open console.firebase.google.com and click your project.
2. In the left menu, open **Firestore Database**. (It may be under **Build** or **Databases & Storage**.)
3. Click the **Rules** tab at the top.
4. You'll see a text box with some code already in it (Firebase's default rules). Click inside it, press Ctrl+A (Cmd+A on Mac) to select all of that code, and press Delete so the box is empty.
   Then, on your computer, open the file `firestore.rules` from this folder with Notepad (Windows) or TextEdit (Mac). Press Ctrl+A and Ctrl+C to copy everything in it. Go back to the Rules box and press Ctrl+V to paste.
5. Click **Publish**.

## 2. Get your Firebase settings

1. In the left menu, click the **gear icon** next to "Project Overview", then **Project settings**.
2. Scroll down to **Your apps**. Click the **`</>`** (Web) icon.
3. Enter a nickname, e.g. `allowance-web`. **Leave "Firebase Hosting" unticked**, then click **Register app**.
4. You'll see code containing `const firebaseConfig = { apiKey: "...", ... }`. Keep this page open.

If you already registered a web app, the same settings are shown under **Your apps > SDK setup and configuration > Config**.

## 3. Paste the settings into index.html

1. Open `index.html` in Notepad (Windows) or TextEdit (Mac).
2. Press Ctrl+F (Cmd+F on Mac) and search for `FIREBASE_CONFIG`.
3. Replace each `PASTE_HERE` with the matching value from Firebase: apiKey, authDomain, projectId, storageBucket, messagingSenderId, and appId. Keep the quote marks.
4. Save the file.

When you're done, it should look like this, with your own values:

```js
const FIREBASE_CONFIG = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abc123"
};
```

## 4. Upload to GitHub

1. Open your `allowance-tracker` repository and click **Add file > Upload files**.
2. Drag in `index.html`, `firestore.rules`, and `README.md`, then click **Commit changes**. The new files replace the old ones.
3. You can delete the old `apps-script` folder from the repo. It's no longer used.

GitHub Pages updates within a minute or two.

## 5. First open: choose the family passcode

Open your site. The first time, it asks for a passcode:

- Choose one with **at least 6 characters** that's hard to guess, e.g. `santos-allowance-88`.
- It will ask "Start a new tracker with it?" Tap **OK**.
- Then tap the gear and set the weekly target, the collection day, the **rotation order** (names in the order they take turns), and the date of the first person's turn.

## Taking turns

- The top of the app shows the next collection date and whose turn it is. **Whose turn** lists the next 6 weeks.
- If the person whose turn it is can't pay, tap **"(name) can't make it"** and choose who's covering. The rotation doesn't change. The amount is recorded as owed back, and it appears under **Owed back**.
- When it's repaid, tap **Paid back** and enter the amount. Covering one of the other person's turns later also counts, so the balance evens out automatically.

Send your siblings the link and the passcode. When they enter the **same** passcode, they'll see the same tracker. If someone mistypes it, the app warns that no tracker uses that passcode, so they won't create a separate one by accident.

To install it like an app: on iPhone, open it in Safari and tap Share > Add to Home Screen. On Android, open it in Chrome and tap the menu > Add to Home screen.

## Good to know

- **Cost:** stays on the free Spark plan. Never add a payment method or upgrade to Blaze.
- **The apiKey is safe to be public.** It only identifies your project, and the rules control access. GitHub may email a "secret detected" alert about it. You can mark that alert as safe.
- **Offline:** changes made without signal are saved on the phone and sync automatically later.
- **Viewing data:** Firebase console > Firestore Database > Data > `families` > your passcode.
- **Changing the passcode:** there's no rename in the app. Start a new tracker with a new passcode, and use "Forget passcode on this phone" in Settings to switch.

## Troubleshooting

- **"Firebase blocked access":** the rules weren't published. Redo step 1, and make sure you clicked **Publish**.
- **The page says "Saved on this device":** `FIREBASE_CONFIG` still contains `PASTE_HERE`. Redo step 3.
- **"Couldn't reach Firebase":** check that `projectId` matches your project exactly, and that Firestore was created (step 1, item 2).
