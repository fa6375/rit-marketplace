# Marketplace — Local Setup Guide

A modern student marketplace built with **React + Firebase (Auth / Firestore / Storage) + Framer Motion + Tailwind CSS**.

---

## 📦 What's included

This zip contains the full **frontend** folder. There is **no backend** — the app talks directly to your Firebase project.

```
frontend/
├── public/
├── src/
│   ├── components/      # Navbar, ListingCard, EmptyState, DragDropImage, …
│   ├── context/         # AuthContext (Firebase auth provider)
│   ├── lib/             # firebase.js + categories.js
│   ├── pages/           # AuthPage, VerifyEmail, Dashboard, CreateListing, …
│   ├── App.js
│   └── index.js
├── package.json
└── tailwind.config.js
firestore.rules          # Firestore security rules
storage.rules            # Firebase Storage security rules
```

---

## ✅ Prerequisites

Install these on your laptop first:

- **Node.js 18+** → https://nodejs.org/
- **Yarn** (recommended) → `npm install -g yarn`
- A modern browser (Chrome / Edge / Firefox / Safari)

---

## 🚀 Run it in 4 steps

```bash
# 1. Open a terminal in the unzipped folder
cd marketplace/frontend

# 2. Install dependencies (one time only, ~1–2 min)
yarn install

# 3. Start the dev server
yarn start

# 4. The app opens automatically at:
#    http://localhost:3000
```

That's it. You'll see the **Marketplace login page** — sign up with your email, click the verification link, and the marketplace is yours.

---

## 🔥 Firebase setup (one-time, ~2 minutes)

Your Firebase project (`rit-marketplace`) is already wired into `src/lib/firebase.js`. You only need to confirm two things in the [Firebase Console](https://console.firebase.google.com/project/rit-marketplace):

### 1. Enable Email/Password Authentication
- Go to **Authentication → Sign-in method**
- Enable **Email/Password**

### 2. Deploy the security rules

**Firestore rules** (Firestore Database → Rules tab):
Copy the contents of `firestore.rules` (in the zip) and click **Publish**.

**Storage rules** (Storage → Rules tab):
Copy the contents of `storage.rules` and click **Publish**.

> Without these rules, users won't be able to create listings or upload images.

---

## 🧪 Testing the flow

1. Run `yarn start` → login page opens at `localhost:3000/login`
2. Click **Create an account**, fill in name + email + password (≥ 6 chars), submit
3. You'll be redirected to `/verify-email`
4. Check your inbox → click the Firebase verification link
5. Return to the app → click **"I have verified — continue"**
6. You're in! Click **Post a listing**, upload an image, add title/price/category → it appears instantly on the dashboard
7. Open the same URL in another browser/incognito to see real-time updates

---

## 🛠️ Build for production

```bash
yarn build
```

This creates an optimized `build/` folder. Deploy it anywhere — Vercel, Netlify, Firebase Hosting, Cloudflare Pages, etc. Example with Firebase Hosting:

```bash
npm install -g firebase-tools
firebase login
firebase init hosting   # choose 'build' as the public dir
firebase deploy
```

---

## ❓ Troubleshooting

| Problem | Fix |
|---|---|
| `Module not found` after install | Delete `node_modules` and run `yarn install` again |
| Verification email never arrives | Check spam. Make sure Email/Password sign-in is enabled in Firebase |
| Can't post a listing (permission error) | Publish the rules from `firestore.rules` and `storage.rules` |
| Port 3000 already in use | Run `PORT=3001 yarn start` |

---

## 📁 Key files to know

- `src/lib/firebase.js` — your Firebase config (already set)
- `src/context/AuthContext.jsx` — auth state, signup, login, verify
- `src/pages/Dashboard.jsx` — real-time listing grid (`onSnapshot`)
- `src/pages/CreateListing.jsx` — drag-drop upload to Firebase Storage
- `firestore.rules` / `storage.rules` — must be deployed to Firebase

Enjoy your marketplace! 🎉
