# Macrogram

A progressive web app (PWA) for tracking daily nutrition macros, body measurements, and meal recipes — built with vanilla JS and Firebase.

## Features

- **Macro Tracking** — log daily calories, protein, carbs, and fat; visualize progress against targets
- **Calendar View** — browse past days and review historical logs
- **Body Measurements** — track weight and other measurements over time
- **Recipes** — save and reuse custom meals with auto-calculated macros
- **Macro Calculator** — personalized targets computed from height, weight, age, activity level, and goal (cut / maintain / bulk)
- **Firebase Auth** — sign in with Google; all data is private per account
- **Firestore** — real-time cloud sync; works offline and syncs when reconnected
- **Installable PWA** — add to home screen on Android (Chrome) and iOS (Safari) for a native-app feel

## Tech Stack

- Vanilla HTML / CSS / JavaScript (single `index.html`)
- Firebase Authentication (Google sign-in)
- Cloud Firestore
- Firebase Hosting
- Web App Manifest + Service Worker for PWA support

## Setup

See [SETUP.md](SETUP.md) for step-by-step instructions to configure Firebase and deploy.

## Deploy

```bash
npm install -g firebase-tools
firebase login
firebase init hosting   # public dir = ".", single-page app = yes
firebase deploy
```

Your app will be live at `https://<project-id>.web.app`.

## License

MIT
