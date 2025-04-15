# Meeting Scheduler

A simple web application that allows users to authenticate with Google SSO and create/schedule Google Meet meetings.

## Features

- Google SSO authentication using NextAuth.js
- Create instant Google Meet meetings
- Schedule future meetings
- Modern UI with Tailwind CSS
- State management with Redux

## Prerequisites

- Node.js 18.x or later
- npm or yarn
- Google Cloud Platform account for OAuth credentials

## Setup

1. Clone the repository:
```bash
git clone https://github.com/OwinoLucas/Meeting_Scheduler.git
cd meeting-scheduler
```

2. Install dependencies:
```bash
npm install
# or
yarn install
```

3. Set up Google OAuth credentials:
   - Go to the [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Enable the Google Calendar API
   - Create OAuth 2.0 credentials
   - Add authorized redirect URIs:
     - http://localhost:3000/api/auth/callback/google
     - https://your-production-domain.com/api/auth/callback/google

4. Create a `.env.local` file in the root directory with the following variables:
```
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
```

5. Run the development server:
```bash
npm run dev
# or
yarn dev
```

6. Open [http://localhost:3000](http://localhost:3000) in your browser.

## Deployment

The application can be deployed to Netlify:

1. Push your code to a Git repository
2. Connect your repository to Netlify
3. Set up the environment variables in Netlify's dashboard
4. Deploy!

## Authentication Troubleshooting

If you encounter OAuthSignin errors with Google authentication, follow these steps:

### 1. Verify Network Connectivity
The ETIMEDOUT error indicates a connection timeout. Ensure your network can reach Google's authentication servers:
- Check your internet connection
- Verify there are no firewall rules or proxy settings blocking access to Google domains
- Try accessing https://accounts.google.com in your browser

### 2. Configure Google Cloud Console
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Select your project (or create one if needed)
3. Navigate to "APIs & Services" > "Credentials"
4. Edit your OAuth 2.0 Client ID or create a new one with these settings:
   - Application type: Web application
   - Name: Meeting Scheduler (or any descriptive name)
   - Authorized JavaScript origins: `http://localhost:3000`
   - Authorized redirect URIs: `http://localhost:3000/api/auth/callback/google`
   - Click "Save"

### 3. Configure OAuth Consent Screen
1. Navigate to "APIs & Services" > "OAuth consent screen"
2. Set up the consent screen if not already done
3. Under "Scopes for Google APIs", add these scopes:
   - `openid`
   - `email`
   - `profile`
   - `https://www.googleapis.com/auth/calendar`
   - `https://www.googleapis.com/auth/calendar.events`

### 4. Enable Google Calendar API
1. Navigate to "APIs & Services" > "Library"
2. Search for "Google Calendar API"
3. Click on it and ensure it's enabled for your project

### 5. Verify Environment Variables
Make sure your `.env.local` file contains:
```
# NextAuth Configuration
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=[your-secret-key]

# Google OAuth Credentials
GOOGLE_CLIENT_ID=[your-client-id]
GOOGLE_CLIENT_SECRET=[your-client-secret]
```

### 6. Clear Browser Cookies 
Clear your browser cookies for localhost to remove any stale authentication data.

### 7. Restart Development Server
```bash
npm run dev
```

## 🔐 Testing Google SSO Login

To test the Google Sign-In functionality with Calendar access, please use the following email:

**✅ Approved Test Email:**  
`lucowish35@gmail.com`

This email has been added as a **Test User** in the Google OAuth Consent Screen configuration. Test Users are able to bypass the "unverified app" warning and can complete the sign-in process with elevated scopes such as:

- `openid`
- `email`
- `profile`
- `https://www.googleapis.com/auth/calendar`
- `https://www.googleapis.com/auth/calendar.events`

---

### ⚠️ Why Your Personal Google Email Might Not Work

If you try to log in using a Google account that is **not listed as a test user**, you may encounter the following warning:

> **Google hasn’t verified this app**  
> The app is requesting access to sensitive info in your Google Account.  
> Until the developer verifies this app with Google, you shouldn't use it.

This is expected behavior when an OAuth app is in **testing mode** and not yet verified by Google. Access to sensitive scopes is restricted to approved test accounts only.

If you need your email added as a test user for evaluation, please contact the developer at: `lucasowino14@gmail.com`.


## Notes

- This is an MVP version without persistent storage
- Meeting links are currently mocked for demonstration purposes
- In a production environment, you would need to implement proper error handling and validation

## License

MIT
