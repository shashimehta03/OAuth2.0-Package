# OAuthClient - OAuth 2.0 Authentication Made Easy

A simple JavaScript library to manage OAuth 2.0 authentication flows with support for generating authorization URLs, handling the callback, exchanging authorization codes for tokens, and refreshing expired tokens.

## Features

- OAuth 2.0 authorization flow integration.
- Token exchange and refresh support.
- Easy integration with Google OAuth endpoints (can be adapted for other OAuth providers).


## Installation

You can install the package using npm:

```bash
npm install oauthclient-noscrubs
```

## Usage

### Importing the Library

To use this package, import the `OAuthClient` class in your project:

```javascript
import OAuthClient from 'oauthclient-noscrubs'; // ES Module

// or
const OAuthClient = require('oauthclient-noscrubs'); // CommonJS
```

### Initialize the OAuth Client

Create a new instance of the `OAuthClient` by passing your OAuth credentials and endpoints:

```javascript
const oauthClient = new OAuthClient({
    clientId: 'your-client-id',
    clientSecret: 'your-client-secret',
    redirectUri: 'your-redirect-uri',
    authEndpoint: 'https://accounts.google.com/o/oauth2/v2/auth',
    tokenEndpoint: 'https://oauth2.googleapis.com/token'
});
```

### Start the Authorization Flow

Generate the authorization URL to redirect the user for OAuth authentication:

```javascript
const authUrl = oauthClient.startAuthFlow();
console.log('Authorization URL:', authUrl);
```

You can redirect the user to this URL or use it in your application to initiate the OAuth flow.

### Handle the Callback

Once the user is redirected back to your app with the authorization code, you can exchange it for tokens:

```javascript
const { code } = req.query;  // Extract the code from the callback URL

try {
    const tokenData = await oauthClient.handleCallback({ code });
    console.log('Token Data:', tokenData);
} catch (error) {
    console.error('Error exchanging code for tokens:', error.message);
}
```

### Fetching User Info

After obtaining the access token, you can use it to fetch user information. Below is an example of how to use the tokens and fetch user info:

```javascript
const tokens = await oauthClient.handleCallback({ code });
const accessToken = tokens.access_token;

// Use the access token to make API calls
try {
    const userInfo = await oauthClient.fetchUserInfo(accessToken);
    console.log('User Info:', userInfo);
} catch (error) {
    console.error('Error fetching user info:', error.message);
}
```

### Refresh the Access Token

If the access token expires, you can use the refresh token to get a new one:

```javascript
try {
    const refreshedTokens = await oauthClient.refreshToken(refreshToken);
    console.log('Refreshed Tokens:', refreshedTokens);
} catch (error) {
    console.error('Error refreshing token:', error.message);
}
```

## Example Project

For a complete example, check out the [OAuth Client Example Project](https://github.com/shashimehta03/Oauth2.0-test).

```
This README should provide clear instructions for users to get started with your `OAuthClient` package.
