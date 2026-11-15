# Rupak Lobby Ledger — Firebase edition

A fresh React + Vite lobby ledger using Firebase Authentication and Cloud Firestore.

## 1. Add Firebase config

Copy `.env.example` to `.env.local` and fill in the six values from Firebase Console → Project settings → Your apps → SDK setup and configuration → Config. Keep the variable names exactly as shown. The web config is intended for client apps; never put a Firebase service-account private key in this project.

## 2. Firebase console

- Authentication → Sign-in method → Email/Password: enabled.
- Firestore Database → Rules: publish the contents of `firestore.rules`.
- Authentication → Settings → Authorized domains: add your Vercel domain (for example `your-site.vercel.app`).

The app stores data under `users/{Firebase UID}/lobbies` and `users/{Firebase UID}/payments`. Each signed-in user can only read/write their own records under the included rules.

## 3. Run locally

```bash
npm install
npm run dev
```

## 4. Deploy on Vercel

Import the GitHub repository as a Vite project. Add these Environment Variables in Vercel (Project → Settings → Environment Variables):

- `VITE_FIREBASE_API_KEY`
- `VITE_FIREBASE_AUTH_DOMAIN`
- `VITE_FIREBASE_PROJECT_ID`
- `VITE_FIREBASE_STORAGE_BUCKET`
- `VITE_FIREBASE_MESSAGING_SENDER_ID`
- `VITE_FIREBASE_APP_ID`

Use the same values as `.env.local`, then redeploy.

## Notes

- This is a new Firebase app; it does not automatically import existing Supabase data. Keep the Supabase project until you have exported and verified any old records you want to retain.
- The payment log and lobby records are private to the currently signed-in account. It does not yet implement separate admin/staff roles or shared team accounts.
- PDF export uses the currently selected month.
