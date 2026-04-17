# Macrogram — Setup Guide
## ~10 minutes total ⏱️

---

## STEP 1 — Create a Firebase Project (Free)

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → name it `macrogram` → disable Google Analytics → **Create project**

---

## STEP 2 — Enable Authentication

1. Sidebar → **Build → Authentication → Get started**
2. Click **Google** under "Sign-in providers"
3. Toggle **Enable** ON
4. Set a **Project support email** (just pick your Gmail address)
5. Click **Save**
6. *(Optional)* Also enable **Email/Password** if you want a fallback login method

---

## STEP 3 — Create a Firestore Database

1. Sidebar → **Build → Firestore Database → Create database**
2. Choose **Start in production mode** → pick a location → **Enable**
3. Click the **Rules** tab, replace with this and click **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

---

## STEP 4 — Get Your Firebase Config

1. Click ⚙️ gear → **Project settings**
2. Scroll to **"Your apps"** → click **</>** (web icon)
3. Name it `macrogram-web` → **Register app**
4. Copy the `firebaseConfig` object — you need these 6 values:
   - `apiKey`
   - `authDomain`
   - `projectId`
   - `storageBucket`
   - `messagingSenderId`
   - `appId`

---

## STEP 5 — Paste Config Into index.html

1. Open **index.html** in a text editor
2. Find `FIREBASE_CONFIG` near the bottom of the `<script>` section
3. Replace each `REPLACE_...` value with your Firebase values
4. Save the file

---

## STEP 6 — Deploy to Firebase Hosting (Free)

This gives you a real HTTPS URL both phones can install from.

### Install Node.js (if you don't have it)
Download from **https://nodejs.org** (LTS version)

### Install Firebase CLI & deploy
Open Terminal (Mac) or Command Prompt (Windows):

```bash
npm install -g firebase-tools
cd path/to/macrogram-folder
firebase login
firebase init hosting
```

When prompted:
- **Use an existing project** → select your `macrogram` project
- **Public directory** → type `.` (just a dot — current folder)
- **Single-page app** → **Yes**
- **Overwrite index.html?** → **No** ← important!

Then deploy:
```bash
firebase deploy
```

You'll get a URL like `https://macrogram-xxxxx.web.app` — **that's your app!**

---

## STEP 7 — Install on Phones

### Android (Samsung Galaxy Z Fold 7)
1. Open **Chrome** → go to your Firebase URL
2. Tap ⋮ menu → **"Add to Home screen"** → **Install**

### iPhone (iOS — for your friend)
1. Open **Safari** (must be Safari, not Chrome)
2. Go to your Firebase URL
3. Tap **Share button** (bottom center) → **"Add to Home Screen"** → **Add**

---

## STEP 8 — Create Accounts

1. Open the app → tap **Register**
2. Share the URL with your friends — each person registers their own account
3. All data is completely private per account

---

## Notes

- **Free tier**: Firebase Spark plan allows 50,000 reads / 20,000 writes per day — plenty for a group of friends
- **Offline**: The app caches locally and syncs when reconnected
- **Your old data**: If you were using the local HTML version, your meal history from the old file can't be migrated automatically since it was stored in your browser's localStorage. You'll start fresh in the cloud version.
- **Sharing macros**: Each user manages their own targets — the 🧮 Calc button auto-calculates personalised targets from height, weight, age, goal and activity level