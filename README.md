# Healthy Habit Calendar

A small habit-tracking web app (PWA). Works on Android and iPhone, offline, and syncs across devices when you sign in with Google.

## Run it on GitHub Pages (free)

1. Create a new **public** repository on GitHub, e.g. `healthy-habits`.
2. Upload all the files in this folder (index.html, manifest.json, sw.js, icon-192.png, icon-512.png).
3. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. After a minute your app is live at `https://<your-username>.github.io/healthy-habits/`.
5. **Important for Google sign-in:** in the Firebase console → Authentication → Settings → Authorized domains → Add domain → `<your-username>.github.io`.

## Install on your phone

- Android (Chrome): open the link → menu (⋮) → Install app / Add to Home screen
- iPhone (Safari): open the link → Share → Add to Home Screen

## Data

- Not signed in: ticks are saved on that device only.
- Signed in with Google: saved in Firestore under `users/<your uid>/…`, and only you can read or write it (see rules below). Data from before sign-in is uploaded once.

Firestore rules in use:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```
