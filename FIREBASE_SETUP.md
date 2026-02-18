# 🔥 Firebase Configuration Guide

## Step-by-Step Setup (15 minutes)

### Step 1: Create Firebase Project

1. Go to **Firebase Console**: https://console.firebase.google.com
2. Click **"Add project"**
3. Enter project name: `volunteerhub`
4. Click **Continue**
5. Disable Google Analytics (optional for hackathon)
6. Click **"Create project"**
7. Wait for setup to complete (30 seconds)

### Step 2: Enable Authentication

1. In left sidebar, click **"Build"** → **"Authentication"**
2. Click **"Get started"** button
3. Click **"Email/Password"** provider
4. Toggle **"Enable"** switch ON
5. Toggle **"Email link (passwordless sign-in)"** OFF (keep it simple)
6. Click **"Save"**

### Step 3: Create Firestore Database

1. In left sidebar, click **"Build"** → **"Firestore Database"**
2. Click **"Create database"** button
3. Select **"Start in test mode"** (radio button)
   - This allows read/write for 30 days (perfect for hackathons)
4. Click **"Next"**
5. Select location closest to you (e.g., `us-central1`)
6. Click **"Enable"**
7. Wait for database creation (1 minute)

### Step 4: Set Firestore Security Rules (For Hackathon)

1. In Firestore Database, click **"Rules"** tab
2. Replace existing rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow all reads and writes for testing
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

3. Click **"Publish"**
4. ⚠️ **Important**: These rules are for development only. For production, implement proper security.

### Step 5: Get Firebase Configuration

1. Click the **gear icon** ⚙️ (top left) → **"Project settings"**
2. Scroll down to **"Your apps"** section
3. Click the **`</>`** icon (Web app)
4. Enter app nickname: `VolunteerHub`
5. **DON'T** check "Also set up Firebase Hosting" (unless you want to deploy)
6. Click **"Register app"**
7. You'll see a code snippet like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyBxxx...",
  authDomain: "volunteerhub-xxx.firebaseapp.com",
  projectId: "volunteerhub-xxx",
  storageBucket: "volunteerhub-xxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

8. **Copy this entire object**
9. Click **"Continue to console"**

### Step 6: Update HTML Files

You need to replace the Firebase config in **ALL 7 HTML files**:

1. `index.html`
2. `profile.html`
3. `ngo.html`
4. `volunteer.html`
5. `dashboard.html`
6. `quiz.html`
7. `map.html`

**Find this section in each file:**

```javascript
// TODO: Replace with your Firebase config
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

**Replace with your actual config** (from Step 5):

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyBxxx...",
    authDomain: "volunteerhub-xxx.firebaseapp.com",
    projectId: "volunteerhub-xxx",
    storageBucket: "volunteerhub-xxx.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abcdef123456"
};
```

### Quick Replace Method

**VS Code:**
1. Press `Ctrl+Shift+H` (Windows) or `Cmd+Shift+H` (Mac)
2. Enable "Replace in Files"
3. Search for: `apiKey: "YOUR_API_KEY"`
4. Replace with: `apiKey: "YOUR_ACTUAL_KEY"`
5. Repeat for each config value

**Find and Replace Values:**
- `YOUR_API_KEY` → Your actual `apiKey`
- `YOUR_PROJECT.firebaseapp.com` → Your actual `authDomain`
- `YOUR_PROJECT_ID` → Your actual `projectId`
- `YOUR_PROJECT.appspot.com` → Your actual `storageBucket`
- `YOUR_SENDER_ID` → Your actual `messagingSenderId`
- `YOUR_APP_ID` → Your actual `appId`

## Verification Checklist

After updating all files, verify:

- [ ] All 7 HTML files have the same Firebase config
- [ ] No "YOUR_API_KEY" placeholders remain
- [ ] Authentication is enabled in Firebase Console
- [ ] Firestore Database is created
- [ ] Firestore rules are set to test mode

## Test Your Setup

1. **Open `index.html` in browser**
2. **Try to Sign Up:**
   - Email: `test@volunteer.com`
   - Password: `password123`
   - Role: Volunteer
   - Click "Sign Up"

3. **Check for Success:**
   - Should redirect to `profile.html`
   - No errors in browser console (F12)

4. **Verify in Firebase Console:**
   - Go to Authentication → Users
   - You should see the new user listed

## Common Errors & Solutions

### Error: "Firebase: Error (auth/invalid-api-key)"
```
Problem: Wrong or missing API key
Solution: Double-check you copied the full apiKey value
```

### Error: "Missing or insufficient permissions"
```
Problem: Firestore rules too strict
Solution: Set rules to test mode (see Step 4)
```

### Error: "Firebase not defined"
```
Problem: Firebase config not in file
Solution: Make sure you updated ALL 7 HTML files
```

### Page doesn't redirect after login
```
Problem: Firestore rules or collection structure
Solution: 
1. Check browser console (F12) for errors
2. Verify Firestore rules allow read/write
3. Make sure you're online
```

## Firestore Database Structure (Auto-Created)

When you use the app, these collections will be created automatically:

```
volunteerhub (project)
├── users/
│   ├── {user-id-1}/
│   │   ├── uid: "abc123"
│   │   ├── email: "test@volunteer.com"
│   │   ├── role: "volunteer"
│   │   ├── name: "John Doe"
│   │   ├── skills: ["teaching", "tech"]
│   │   └── interests: ["education", "health"]
│   └── {user-id-2}/
│       └── ...
├── opportunities/
│   ├── {opp-id-1}/
│   │   ├── title: "Math Tutors Needed"
│   │   ├── ngoName: "Education First"
│   │   ├── skills: ["teaching", "math"]
│   │   ├── urgent: true
│   │   └── micro: true
│   └── ...
└── applications/
    ├── {app-id-1}/
    │   ├── volunteerId: "abc123"
    │   ├── opportunityId: "xyz789"
    │   └── status: "pending"
    └── ...
```

## Production Deployment (Bonus)

If you want to deploy to Firebase Hosting:

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize Firebase in project folder
cd volunteer-platform
firebase init

# Select:
# - Hosting
# - Use existing project: volunteerhub
# - Public directory: . (current folder)
# - Single-page app: No
# - Don't overwrite files

# Deploy
firebase deploy

# Your app will be live at:
# https://volunteerhub-xxx.web.app
```

## Security Rules for Production

Replace test rules with secure rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can read/write their own data
    match /users/{userId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Anyone can read opportunities
    match /opportunities/{oppId} {
      allow read: if true;
      allow create: if request.auth != null;
      allow update, delete: if request.auth != null && 
                              resource.data.ngoId == request.auth.uid;
    }
    
    // Applications
    match /applications/{appId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update: if request.auth != null && 
                       resource.data.volunteerId == request.auth.uid;
    }
  }
}
```

## Need Help?

**Firebase Documentation:**
- Auth: https://firebase.google.com/docs/auth/web/start
- Firestore: https://firebase.google.com/docs/firestore/quickstart

**Quick Support:**
1. Check browser console (F12) for error messages
2. Verify Firebase config is correct in all files
3. Make sure internet connection is active
4. Try incognito/private browsing mode

---

**Setup Complete! 🎉**

You're ready to build your volunteer matching platform!
