# Vue Firebase App

This is a Vue 3 application built with Vite that implements task storage using Firebase. It supports features like user Create Task, Read Task, Edit/Update Task and Delete Task with integration to Firestore for managing task-related data.

## 🚀 Features

- Firestore Database Integration
- Environment variable support with Vite

## 🔧 Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/vue-firebase-auth.git
cd vue-firebase-auth

2. Install Dependencies
npm install

3. Environment Configuration
Create a .env file in the root of your project and add your Firebase project credentials:

VITE_FIREBASE_API_KEY=your-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your-messaging-sender-id
VITE_FIREBASE_APP_ID=your-app-id
⚠️ Make sure all variable names start with VITE_ so they can be accessed in the client.

4. Run the App

npm run dev


📁 Folder Structure

src/
├── components/      # Reusable Vue components
├── firebase.js      # Firebase configuration and initialization
└── main.js          # App entry point


📚 Tech Stack
Vue 3

Vite

Firebase

BootsrapCSS


📌 Notes
Remember to restart your dev server after changing .env files.

Avoid committing .env files or Firebase secrets to version control.