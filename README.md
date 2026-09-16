TEST_PASTE_1234# 🇶🇦 Visa Aylin Consultancy - Qatar Job Hunt Tracker

A professional webapp for tracking Qatar job hunt progress. Free hosting on GitHub Pages + Firebase for authentication and data sync.

**Live demo:** Will be at `https://YOUR_USERNAME.github.io/visa-aylin/`

---

## 📋 What's Included

- ✅ Google Sign-In (Gmail) — users log in with one click
- ✅ Real-time progress sync across devices
- ✅ Admin dashboard — you see every user's progress live
- ✅ WhatsApp share for user progress reports
- ✅ CSV export for follow-up campaigns
- ✅ Deadline tracking with overdue alerts
- ✅ Mobile-first responsive design
- ✅ 100% free to run (GitHub + Firebase free tier)

---

## 🚀 Complete Setup Guide (30 minutes)

Follow these steps **in order**. Do not skip.

### Part 1: Create Firebase Project (10 minutes)

Firebase is Google's free backend service. It handles user login and data storage.

#### 1.1 Create a Firebase Project
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Sign in with your Google account (`seridifac@outlook.fr` if it's linked to Google, otherwise create a Gmail)
3. Click **"Add project"** (or "Create a project")
4. Project name: `visa-aylin` (or anything you like)
5. Disable Google Analytics (not needed) → Click **Continue** → **Create project**
6. Wait ~30 seconds, then click **Continue**

#### 1.2 Enable Google Authentication
1. In the left sidebar, click **Build → Authentication**
2. Click **"Get started"**
3. Under "Sign-in method" tab, click **Google**
4. Toggle **Enable**
5. Set **Project public-facing name:** `Visa Aylin Consultancy`
6. Set **Project support email:** your email
7. Click **Save**

#### 1.3 Create Firestore Database
1. In the left sidebar, click **Build → Firestore Database**
2. Click **"Create database"**
3. Choose **"Start in production mode"** → Next
4. Choose location: **`eur3` (europe-west)** — closest to Qatar/Algeria
5. Click **Enable**
6. Wait ~1 minute for database to be created

#### 1.4 Deploy Security Rules
1. In Firestore, click the **"Rules"** tab (top)
2. **Delete everything** in the editor
3. Copy-paste this entire block:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /trackers/{userId} {
      // Any signed-in user can read all trackers (needed for admin dashboard)
      // In production, replace with admin-only read
      allow read: if request.auth != null;
      // Users can only write their own tracker
      allow write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

4. Click **Publish**

> ⚠️ **Security note:** These rules let any signed-in user read all trackers. For a small trusted group this is fine. For production with untrusted users, we should tighten this — ask me.

#### 1.5 Get Your Firebase Config
1. In Firebase console, click the **⚙️ gear icon** (top-left) → **Project settings**
2. Scroll down to **"Your apps"**
3. Click the **`</>`** (Web) icon
4. App nickname: `Visa Aylin Web`
5. **Do NOT** check "Also set up Firebase Hosting"
6. Click **Register app**
7. You'll see code like this — **copy the entire `firebaseConfig` object**:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "visa-aylin.firebaseapp.com",
  projectId: "visa-aylin",
  storageBucket: "visa-aylin.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

**⚠️ SAVE THIS — you'll need it in Part 2**

8. Click **Continue to console** (you can ignore the SDK setup steps)

---

### Part 2: Configure the Webapp (5 minutes)

#### 2.1 Open `index.html` in a Text Editor
Use Notepad, VS Code, TextEdit, or any text editor.

#### 2.2 Find the Firebase Config Section (around line 340)
Look for:
```javascript
// 🔧 FIREBASE CONFIGURATION - REPLACE WITH YOUR OWN
const firebaseConfig = {
  apiKey: "PASTE_YOUR_API_KEY_HERE",
  ...
};
```

#### 2.3 Replace with Your Real Config
Paste the config you copied from Firebase in step 1.5. Make sure the format matches (with quotes around values).

#### 2.4 Verify Admin Email (around line 355)
```javascript
const ADMIN_EMAILS = [
  "seridifac@outlook.fr"  // ← Should be your Google-connected email
];
```

> ⚠️ **Important:** Use the email tied to your **Google account** here. If you sign in with a different Google account, it won't be recognized as admin. If your Outlook email isn't linked to Google, create a Gmail and use that instead.

#### 2.5 Save the file

---

### Part 3: Deploy to GitHub Pages (10 minutes)

#### 3.1 Create a GitHub Account
1. Go to [github.com](https://github.com) → Sign up
2. Verify your email

#### 3.2 Create a New Repository
1. Click the **`+`** icon top-right → **New repository**
2. Repository name: `visa-aylin`
3. Description: `Qatar Job Hunt Tracker`
4. Select **Public**
5. Check **"Add a README file"**
6. Click **Create repository**

#### 3.3 Upload Your Files
1. On your new repo page, click **"Add file"** → **"Upload files"**
2. Drag and drop these 3 files:
   - `index.html` (your configured version)
   - `firestore.rules`
   - `PRIVACY.md`
3. Scroll down → Commit message: `Initial launch` → **Commit changes**

#### 3.4 Enable GitHub Pages
1. Click **Settings** (top of repo)
2. In left sidebar, click **Pages**
3. Under **"Source"**, select **"Deploy from a branch"**
4. Branch: **main** / Folder: **`/ (root)`** → **Save**
5. Wait 1-2 minutes
6. Refresh — you'll see: **"Your site is live at `https://YOUR_USERNAME.github.io/visa-aylin/`"**

#### 3.5 Add Your Domain to Firebase Authorized Domains
1. Copy your GitHub Pages URL (e.g. `YOUR_USERNAME.github.io`)
2. Go to Firebase Console → **Authentication → Settings → Authorized domains**
3. Click **"Add domain"**
4. Paste: `YOUR_USERNAME.github.io` (without `https://` or path)
5. Click **Add**

---

### Part 4: Test Everything (5 minutes)

1. Open your live URL in a browser
2. Click **"Sign in with Google"**
3. Sign in with your admin email (`seridifac@outlook.fr` or your Google email)
4. You should see **📋 My Tasks** and **👥 Team Dashboard** toggle at the top
5. Click a few tasks to mark them done
6. Open the URL in a different browser (or incognito) with a different Google account
7. Complete a few tasks as that user
8. Go back to admin browser → click **Team Dashboard** → you should see both users listed

**✅ If this works, you're live!**

---

## 📣 Sharing With Job Hunters

Once live, share your URL in WhatsApp:

```
🇶🇦 *VISA AYLIN CONSULTANCY*
Your Qatar Job Hunt Tracker

1. Open: https://YOUR_USERNAME.github.io/visa-aylin/
2. Sign in with your Google account
3. Set your travel date
4. Start ticking off your tasks

Every task saves automatically.
Tap "Share Now" to send me your progress.

Yalla, Qatar is waiting! 💪
```

---

## 🔧 How to Update the App Later

To change any code (add tasks, update contact info, etc.):

1. Go to your GitHub repo → click `index.html`
2. Click the **✏️ pencil icon** (top-right of file view)
3. Edit as needed
4. Scroll down → Commit message → **Commit changes**
5. Changes go live within 1-2 minutes

---

## 💰 Costs

- **GitHub Pages:** Free forever
- **Firebase Free Tier:**
  - 50,000 reads/day
  - 20,000 writes/day
  - 1 GB storage
  - 10 GB bandwidth/month
- **For your use case:** Easily supports 500+ active users on free tier

**Set a spending alert at $0 in Firebase to be safe:**
1. Firebase Console → ⚙️ → **Usage and billing** → **Details & settings**
2. Set budget alert at **$1** (you'll get an email if anything is charged)

---

## 🆘 Troubleshooting

**"Firebase: Error (auth/unauthorized-domain)"**
→ You forgot Part 3.5. Add your GitHub URL to Firebase authorized domains.

**"Missing or insufficient permissions"**
→ Firestore rules not deployed. Redo Part 1.4.

**Admin dashboard not showing**
→ Your login email doesn't match `ADMIN_EMAILS` in the code. Check spelling and case.

**"Sign in failed"**
→ Google Auth not enabled. Redo Part 1.2.

---

## 📊 What to Do Once You Have Users

1. **Weekly WhatsApp broadcasts** — remind them of upcoming deadlines
2. **Export CSV** — download all users, follow up with the least active ones
3. **Add testimonials** — get quotes from successful placements
4. **Introduce paid tiers** — CV review, coaching, employer intros
5. **Buy custom domain** — `visaaylin.com` for professional branding

---

## 📞 Contact & Support

**Visa Aylin Consultancy**
- WhatsApp: +974 6634 5802
- Email: seridifac@outlook.fr

---

_Built with Firebase + GitHub Pages. Powered by determination. 🇶🇦_
