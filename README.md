# 🤝 VolunteerHub - Volunteer-NGO Matching Platform

A smart platform that connects volunteers with NGOs based on skills, interests, and availability. Built for hackathons with Firebase integration.

## 🌟 Features

### Core Features (Must-Have)
1. **Authentication System** (`index.html`)
   - Email/password login and signup
   - Role-based routing (Volunteer/NGO)
   - Firebase Authentication integration

2. **Volunteer Profile** (`profile.html`)
   - Complete profile setup
   - Skills selection
   - Interests and availability
   - Profile completion tracking

3. **NGO Dashboard** (`ngo.html`)
   - Post volunteer opportunities
   - Mark micro-volunteering tasks (30-60 min)
   - Flag urgent needs
   - View posted opportunities

4. **Smart Volunteer Feed** (`volunteer.html`) ⭐ **MAIN PAGE**
   - AI-powered skill matching
   - Priority sorting (Urgent → Micro → Match score)
   - Filter by urgent, quick tasks, or matched skills
   - One-click application
   - Visual badges for matched skills

5. **Impact Dashboard** (`dashboard.html`)
   - Hours contributed tracker
   - Tasks completed counter
   - Causes supported visualization
   - Personalized impact messages
   - Application history

### Bonus Features
6. **Cause Discovery Quiz** (`quiz.html`)
   - 4-question personality quiz
   - Smart cause matching algorithm
   - Skill recommendations
   - Results saved to profile

7. **NGO Map View** (`map.html`)
   - Visual map of NGOs (Google Maps iframe)
   - List of active NGOs
   - Skills needed by location
   - Direct links to opportunities

## 🚀 Quick Setup

### Prerequisites
- Web browser
- Firebase account (free)
- Text editor

### Firebase Setup (10 minutes)

1. **Create Firebase Project**
   ```
   1. Go to https://console.firebase.google.com
   2. Click "Add project"
   3. Name: "volunteerhub" (or any name)
   4. Disable Google Analytics (optional)
   5. Click "Create project"
   ```

2. **Enable Authentication**
   ```
   1. In Firebase Console → Build → Authentication
   2. Click "Get started"
   3. Enable "Email/Password" provider
   4. Save
   ```

3. **Create Firestore Database**
   ```
   1. In Firebase Console → Build → Firestore Database
   2. Click "Create database"
   3. Select "Start in test mode" (for development)
   4. Choose a location (closest to you)
   5. Click "Enable"
   ```

4. **Get Firebase Config**
   ```
   1. Project Settings (gear icon) → General
   2. Scroll to "Your apps"
   3. Click </> (Web app icon)
   4. Register app name: "VolunteerHub"
   5. Copy the firebaseConfig object
   ```

5. **Update All HTML Files**
   
   Replace this in ALL 7 HTML files:
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT.firebaseapp.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT.appspot.com",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```

   With your actual config from Firebase Console.

### Running the App

1. **Option A: Local File (Quick Test)**
   ```
   Simply open index.html in your browser
   ```

2. **Option B: Local Server (Recommended)**
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js
   npx http-server
   
   # Then open http://localhost:8000
   ```

3. **Option C: Firebase Hosting (Production)**
   ```bash
   npm install -g firebase-tools
   firebase login
   firebase init hosting
   firebase deploy
   ```

## 📁 File Structure

```
volunteer-platform/
├── index.html          # Login/Signup (START HERE)
├── profile.html        # Volunteer profile setup
├── volunteer.html      # Main feed (JUDGES LOVE THIS)
├── ngo.html           # NGO dashboard
├── dashboard.html     # Impact tracker
├── quiz.html          # Cause discovery (BONUS)
├── map.html           # NGO map (BONUS)
└── css/
    └── style.css      # All styles
```

## 🎯 How to Demo (Hackathon Presentation)

### Setup Before Demo (5 min)
1. Create 2 test accounts:
   - volunteer@test.com (Volunteer)
   - ngo@test.com (NGO)

2. As NGO:
   - Post 3-4 opportunities
   - Mark 1-2 as urgent
   - Mark 1-2 as micro-volunteering

3. As Volunteer:
   - Complete profile with skills
   - Apply to 2-3 opportunities

### Demo Flow (3 minutes)
```
1. START: Show problem (60 sec)
   "Volunteers struggle to find opportunities that match their skills"

2. SOLUTION: Show volunteer feed (90 sec)
   - Smart matching with badges
   - Urgent tasks highlighted
   - One-click apply
   - Filters working

3. IMPACT: Show dashboard (30 sec)
   - "You've contributed 12 hours to Education & Health"
   - Visual impact metrics

4. BONUS: Quick show quiz & map (if time)
```

## 🔥 Judge-Winning Features to Highlight

### Technical
- **Smart Matching Algorithm**: Intersection of volunteer skills ∩ opportunity skills
- **Priority Sorting**: Urgent → Micro → Match count
- **Real-time Updates**: Firebase Firestore
- **Responsive Design**: Mobile-first approach

### User Experience
- **Visual Feedback**: Matched skills highlighted in green
- **Emotional Impact**: Personalized messages
- **Quick Actions**: One-click volunteer
- **Filters**: Urgent/Quick/Matched toggles

### Social Impact
- **Micro-volunteering**: 30-60 min tasks lower barrier to entry
- **Emergency Response**: Urgent flag for disaster relief
- **Skill Development**: Cause quiz suggests skills to learn
- **Geographic Discovery**: Map view connects local volunteers

## 🏆 Hackathon Judging Criteria Alignment

| Criteria | How We Score |
|----------|-------------|
| **Impact** | Connects underserved NGOs with skilled volunteers |
| **Innovation** | Smart matching + micro-volunteering concept |
| **Technical** | Firebase integration, matching algorithm |
| **Design** | Clean UI, emotional dashboard, visual badges |
| **Completeness** | 5 core pages + 2 bonus features |

## 🛠️ Customization Tips

### Change Color Scheme
Edit `css/style.css`:
```css
:root {
    --primary: #6366f1;  /* Change to your color */
    --secondary: #10b981;
}
```

### Add More Skills
Edit the skills checkboxes in:
- `profile.html`
- `ngo.html`

### Modify Quiz Logic
Edit `quiz.html` → `causeMap` object

### Change Map Location
Edit `map.html` → Update iframe `src` URL

## 📊 Firestore Collections Structure

```
users/
  {uid}/
    - email
    - role: "volunteer" | "ngo"
    - name (volunteers)
    - skills: []
    - interests: []
    - availability
    - preferredCause (from quiz)

opportunities/
  {id}/
    - ngoName
    - title
    - description
    - skills: []
    - location
    - micro: boolean
    - urgent: boolean
    - ngoId
    - createdAt

applications/
  {id}/
    - opportunityId
    - volunteerId
    - appliedAt
    - status: "pending" | "accepted" | "completed"
```

## 🐛 Common Issues & Fixes

### Firebase Config Not Working
```
❌ Error: Firebase not defined
✅ Fix: Make sure you replaced the config in ALL HTML files
```

### Login Redirects to Wrong Page
```
❌ Stuck on profile.html
✅ Fix: Check Firestore rules allow read/write in test mode
```

### Opportunities Not Loading
```
❌ Empty feed
✅ Fix: 
   1. Log in as NGO
   2. Post at least one opportunity
   3. Log in as volunteer
```

### Skills Not Matching
```
❌ No green badges
✅ Fix: Make sure volunteer skills match opportunity skills exactly
```

## 📱 Mobile Responsive

All pages are mobile-responsive with breakpoints at:
- Desktop: > 768px
- Tablet: 768px
- Mobile: < 768px

## 🎨 Design Features

- **Gradient Background**: Purple gradient for modern look
- **Card-based Layout**: Clean, scannable content
- **Badge System**: Visual indicators for status
- **Hover Effects**: Interactive feedback
- **Emoji Icons**: Friendly, approachable UI

## 🚀 Future Enhancements (Post-Hackathon)

- [ ] Real-time chat between volunteers and NGOs
- [ ] Gamification with badges and levels
- [ ] Integration with Google Calendar
- [ ] SMS notifications for urgent tasks
- [ ] Blockchain-verified volunteer hours
- [ ] AI recommendations using ML

## 📄 License

Free to use for hackathons and educational purposes.

## 👥 Team Credits

Built with ❤️ for [Your Hackathon Name]

---

## ⚡ Quick Start Checklist

- [ ] Create Firebase project
- [ ] Enable Email/Password auth
- [ ] Create Firestore database
- [ ] Copy Firebase config
- [ ] Replace config in all 7 HTML files
- [ ] Open index.html in browser
- [ ] Create test accounts (volunteer + NGO)
- [ ] Post opportunities as NGO
- [ ] Apply as volunteer
- [ ] Check dashboard for impact
- [ ] Practice demo (3 min)

**Good luck at your hackathon! 🎉**
