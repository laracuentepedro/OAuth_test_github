# GitHub OAuth App

A Node.js web application demonstrating GitHub OAuth 2.0 authentication using Passport.js. This project showcases how to implement secure user authentication with GitHub's OAuth service, allowing users to log in with their GitHub accounts.

## 🔐 OAuth Implementation Overview

This application implements the OAuth 2.0 authorization code flow with GitHub as the identity provider. The authentication process follows these steps:

1. **User initiates login** - User clicks "Login with GitHub"
2. **Authorization request** - App redirects user to GitHub's authorization server
3. **User consent** - User grants permission to the app
4. **Authorization code** - GitHub redirects back with an authorization code
5. **Token exchange** - App exchanges the code for an access token
6. **User data retrieval** - App uses the token to fetch user profile information
7. **Session creation** - User is logged in and session is established

## 🚀 Features

- **GitHub OAuth Integration** - Secure authentication using GitHub accounts
- **Session Management** - Persistent user sessions with Express Session
- **Protected Routes** - Authentication middleware to protect sensitive pages
- **User Profile Display** - Shows authenticated user's GitHub profile information
- **Responsive UI** - Clean, mobile-friendly interface

## 📋 Prerequisites

Before running this application, you need:

- Node.js (v14 or higher)
- A GitHub account
- A GitHub OAuth App (see setup instructions below)

## ⚙️ GitHub OAuth App Setup

1. **Create a GitHub OAuth App:**
   - Go to GitHub Settings → Developer settings → OAuth Apps
   - Click "New OAuth App"
   - Fill in the application details:
     - **Application name**: Your app name
     - **Homepage URL**: `http://localhost:3000`
     - **Authorization callback URL**: `http://localhost:3000/auth/github/callback`

2. **Get your credentials:**
   - After creating the app, note down the `Client ID`
   - Generate a new `Client Secret`

## 🛠️ Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd github-oauth-app
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Environment configuration:**
   Create a `.env` file in the root directory:
   ```env
   GITHUB_CLIENT_ID=your_github_client_id_here
   GITHUB_CLIENT_SECRET=your_github_client_secret_here
   ```

4. **Start the application:**
   ```bash
   # Development mode (with auto-restart)
   npm run dev
   
   # Production mode
   npm start
   ```

5. **Access the application:**
   Open your browser and navigate to `http://localhost:3000`

## 🏗️ Project Structure

```
├── app.js              # Main application file with OAuth configuration
├── package.json        # Dependencies and scripts
├── .env               # Environment variables (create this)
├── views/             # EJS templates
│   ├── index.ejs      # Home page
│   ├── login.ejs      # Login page
│   ├── account.ejs    # Protected user account page
│   └── layout.ejs     # Base layout template
└── public/            # Static assets (CSS, images, etc.)
```

## 🔧 Key OAuth Components

### Passport Strategy Configuration
The app uses `passport-github2` strategy for GitHub OAuth:

```javascript
passport.use(new GitHubStrategy({
  clientID: GITHUB_CLIENT_ID,
  clientSecret: GITHUB_CLIENT_SECRET,
  callbackURL: "http://localhost:3000/auth/github/callback"
}, function(accessToken, refreshToken, profile, done) {
  return done(null, profile);
}));
```

### Authentication Routes
- `GET /auth/github` - Initiates OAuth flow
- `GET /auth/github/callback` - Handles OAuth callback
- `GET /logout` - Terminates user session

### Protected Routes
Routes protected by the `ensureAuthenticated` middleware:
- `GET /account` - User profile page (requires authentication)

## 🔒 Security Features

- **Environment Variables** - Sensitive credentials stored securely
- **Session Management** - Secure session handling with Express Session
- **CSRF Protection** - Built-in protection through Passport.js
- **Scope Limitation** - Requests only necessary user permissions

## 🎯 OAuth Scopes

The application requests the following GitHub scopes:
- `user` - Access to user profile information

## 🚦 Usage Flow

1. **Visit the home page** - Shows welcome message for unauthenticated users
2. **Click "Login"** - Redirects to GitHub OAuth authorization
3. **Authorize the app** - Grant permissions on GitHub
4. **Access protected content** - View account page with profile information
5. **Logout** - Terminate session and return to home page

## 🛡️ Error Handling

The application includes error handling for:
- Failed OAuth authentication (redirects to login page)
- Missing environment variables
- Network connectivity issues
- Invalid or expired tokens

## 📚 Dependencies

- **express** - Web application framework
- **passport** - Authentication middleware
- **passport-github2** - GitHub OAuth strategy
- **express-session** - Session management
- **ejs** - Template engine
- **dotenv** - Environment variable management

## 🔄 Development

For development with auto-restart:
```bash
npm run dev
```

This uses `nodemon` to automatically restart the server when files change.

## 📝 Notes

- The callback URL must match exactly what's configured in your GitHub OAuth App
- Keep your client secret secure and never commit it to version control
- The session secret should be changed to a secure random string in production
- For production deployment, update the callback URL to match your domain

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is licensed under the ISC License.
