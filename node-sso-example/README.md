
# WorkOS SSO Demo App – Okta + Node.js

This is a simple demo app built in Node.js to test SAML-based Single Sign-On (SSO) integration using WorkOS as the identity abstraction layer and Okta as the Identity Provider (IdP).

## Technologies Used

- Node.js
- Express.js
- JS
- WorkOS Node SDK
- Okta (SAML IdP)

---

## Prerequisites

1. Node.js v22+
2. A WorkOS account
3. An Okta developer account
4. Git

---

## Local Setup Instructions

### 1. Clone the Repository

```
git clone https://github.com/pandresss/workos-sso-demoapp-ps.git
cd workos-sso-demoapp-ps
```

### 2. Install Dependencies

```
npm install
```

### 3. Create a `.env` File

At the root of the project (`node-sso-example/`), create a file named `.env` and populate it as follows:

```
WORKOS_API_KEY=sk_test_...
WORKOS_CLIENT_ID=client_...
PORT=3000
```

(Use your actual values from your WorkOS project dashboard.)

### 4. Start the Server

```
npm start
```

If you get an "address already in use" error, make sure nothing else is running on port 3000.

---

## Setting up WorkOS

### 1. Create an Organization in WorkOS
- Go to your WorkOS dashboard.
- Create a new Organization (e.g., "OKta Tester Connection").
- Note the `Organization ID` (e.g., `org_......).

### 2. Create a SAML Connection
- Choose **SAML** as the connection type.
- Select Okta as your IdP.
- Provide the required SAML metadata from Okta.

---

## Setting up Okta

### 1. Create a New App Integration
- Application type: SAML 2.0
- Single Sign-On URL: `http://localhost:3000/callback`
- Audience URI: Your WorkOS Client ID

### 2. Assign Users
- Assign a test user to the app who has a domain matching your organization (e.g., `user@galusaenterprisesfuel.com`).

### 3. Upload Metadata to WorkOS
- Download the metadata XML from Okta and upload it into your WorkOS SAML Connection settings.

---

## Running the SSO Flow

1. Visit `http://localhost:3000`
2. Select "SAML" as the login method
3. You’ll be redirected to Okta
4. After authentication, you’ll be redirected back and see your user profile info including first and last name

---

## Notes / Common Issues

- If you see a `connection_invalid` error: verify the connection ID in your code matches the one from WorkOS.
- If you see a `profile_not_allowed_outside_organization` error: ensure your test user’s domain matches the domain listed in your WorkOS organization.
- If your app doesn’t restart, make sure another app isn't already using port 3000.




