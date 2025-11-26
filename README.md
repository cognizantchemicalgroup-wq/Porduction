# CCPL Tank Operations System

A comprehensive tank operations management system for Cognizant Chemical Pvt. Ltd.

## Features

- 3D Tank Visualization with Three.js
- Daily Stock Entry and Management
- Production Tracking
- PDF Report Generation
- Mobile-Responsive Design
- Secure Login System
- **Firebase Integration** - Full CRUD operations with real-time updates
- **Edit & Delete Entries** - Modify or remove existing stock entries
- **Automatic Date/Time Tracking** - Date and time automatically saved with each entry

## Deployment to Vercel

### Quick Deploy

1. **Rename the file:**
   - Rename `files - code1.html` to `index.html`

2. **Deploy via Vercel CLI:**
   ```bash
   npm i -g vercel
   vercel
   ```

3. **Or deploy via Vercel Dashboard:**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your repository or drag & drop the `index.html` file
   - Deploy!

### File Structure for Vercel

```
.
├── index.html          (your main HTML file)
├── vercel.json         (Vercel configuration)
└── README.md          (this file)
```

## Firebase Setup (Required for CRUD Operations)

**IMPORTANT:** Before using the application, you must set up Firebase to enable full CRUD functionality.

1. See **[FIREBASE_SETUP.md](./FIREBASE_SETUP.md)** for detailed setup instructions
2. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/)
3. Enable Firestore Database
4. Copy your Firebase configuration
5. Update the `firebaseConfig` object in `index.html` with your credentials

Without Firebase setup, the app will fall back to localStorage (data stored locally on each device only).

## Important Notes

- **External Dependencies:** The app uses CDN resources (Three.js, jsPDF, Firebase) which will load from the internet
- **Data Storage:** 
  - **With Firebase:** Data is stored in cloud Firestore with real-time sync across devices
  - **Without Firebase:** Falls back to browser localStorage (local only)
- **Login Credentials:**
  - production1 / prod1@2024
  - production2 / prod2@2024
  - production3 / prod3@2024
  - production4 / prod4@2024
  - production5 / prod5@2024

## Alternative Hosting Options

If you prefer simpler hosting:

1. **Netlify Drop** - Just drag and drop the HTML file
2. **GitHub Pages** - Free static hosting
3. **Surge.sh** - Simple static hosting
4. **Firebase Hosting** - Google's hosting service

## Browser Requirements

- Modern browser with JavaScript enabled
- WebGL support for 3D visualization
- LocalStorage support for data persistence

