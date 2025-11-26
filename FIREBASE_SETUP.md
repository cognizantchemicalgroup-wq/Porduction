# Firebase Setup Instructions

This guide will help you set up Firebase for your Production Stock Entry website to enable full CRUD (Create, Read, Update, Delete) functionality with real-time updates.

## Prerequisites

- A Google account
- Access to the Firebase Console

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"** or **"Create a project"**
3. Enter a project name (e.g., "CCPL-Tank-Operations")
4. Click **"Continue"**
5. (Optional) Disable Google Analytics if you don't need it, or enable it if you want analytics
6. Click **"Create project"**
7. Wait for the project to be created, then click **"Continue"**

## Step 2: Enable Firestore Database

1. In your Firebase project dashboard, click on **"Firestore Database"** in the left sidebar
2. Click **"Create database"**
3. Select **"Start in test mode"** (for development) or **"Start in production mode"** (for production with security rules)
4. Choose a location for your database (select the closest region to your users)
5. Click **"Enable"**

### Important: Set Up Security Rules

For production use, you should set up proper security rules. Click on the **"Rules"** tab in Firestore and update them:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write access to stock entries
    match /stockEntries/{entryId} {
      allow read, write: if request.auth != null; // Requires authentication
      // OR for public access (less secure):
      // allow read, write: if true;
    }
    
    match /productionEntries/{entryId} {
      allow read, write: if request.auth != null;
      // OR for public access:
      // allow read, write: if true;
    }
  }
}
```

**Note:** For testing purposes, you can use `allow read, write: if true;` but this is NOT secure for production. For production, implement proper authentication.

## Step 3: Get Your Firebase Configuration

1. In your Firebase project dashboard, click on the **gear icon** (⚙️) next to "Project Overview"
2. Select **"Project settings"**
3. Scroll down to the **"Your apps"** section
4. Click on the **Web icon** (`</>`) to add a web app
5. Register your app with a nickname (e.g., "CCPL Web App")
6. Click **"Register app"**
7. Copy the `firebaseConfig` object that appears

## Step 4: Update Your HTML File

1. Open `index.html` in a text editor
2. Find the section that says:
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_AUTH_DOMAIN",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_STORAGE_BUCKET",
       messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```
3. Replace the placeholder values with your actual Firebase configuration values from Step 3

## Step 5: Test Your Setup

1. Open `index.html` in a web browser
2. Log in with your credentials
3. Create a new stock entry by filling in the form and clicking **"Save Snapshot"**
4. Check your Firebase Console → Firestore Database to see if the entry was created
5. Try editing an entry by clicking the **"Edit"** button on any entry
6. Try deleting an entry by clicking the **"Delete"** button

## Step 6: Enable Authentication (Optional but Recommended)

For production use, you should enable Firebase Authentication:

1. In Firebase Console, go to **"Authentication"**
2. Click **"Get started"**
3. Enable **"Email/Password"** or other authentication methods
4. Update your security rules to require authentication (as shown in Step 2)

## Features Implemented

✅ **Create**: New stock entries are saved to Firebase  
✅ **Read**: All entries are loaded from Firebase in real-time  
✅ **Update**: Edit button allows you to modify existing entries (replaces, doesn't create new)  
✅ **Delete**: Delete button removes entries from Firebase  
✅ **Real-time Updates**: Changes are reflected immediately across all connected devices  
✅ **Auto Date/Time**: Date and time are automatically saved with each entry  

## Troubleshooting

### Firebase not initializing
- Check browser console for errors
- Verify your Firebase configuration values are correct
- Ensure you have an internet connection
- Check that Firestore is enabled in your Firebase project

### Entries not appearing
- Check Firestore security rules
- Verify you're looking at the correct collection (`stockEntries`)
- Check browser console for error messages

### Edit/Delete not working
- Ensure Firebase is properly initialized
- Check that the entry has an `id` field (Firebase-generated entries have this)
- Verify security rules allow write access

### Real-time updates not working
- Check browser console for errors
- Verify `onSnapshot` listener is set up correctly
- Ensure Firestore is enabled and accessible

## Data Structure

Entries are stored in Firestore with the following structure:

```
stockEntries (collection)
  └── {documentId}
      ├── operator: string
      ├── shift: string
      ├── remarks: string
      ├── data: array of tank objects
      ├── total: number
      ├── timestamp: string (ISO format)
      ├── dateTime: string (ISO format)
      ├── displayTime: string (localized)
      ├── createdAt: timestamp
      └── updatedAt: timestamp
```

## Support

If you encounter any issues:
1. Check the browser console (F12) for error messages
2. Verify your Firebase configuration
3. Check Firestore security rules
4. Ensure Firestore is enabled in your Firebase project

## Security Best Practices

1. **Never commit your Firebase config with real credentials to public repositories**
2. **Use environment variables or a config file that's excluded from version control**
3. **Set up proper security rules** - don't use `allow read, write: if true;` in production
4. **Enable Firebase Authentication** for production use
5. **Regularly review your Firestore security rules**
6. **Monitor your Firebase usage** to avoid unexpected costs

## Cost Considerations

Firebase Firestore has a free tier that includes:
- 50,000 reads/day
- 20,000 writes/day
- 20,000 deletes/day
- 1 GB storage

For most small to medium operations, this should be sufficient. Monitor your usage in the Firebase Console.

