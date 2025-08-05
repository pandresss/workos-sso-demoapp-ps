# WorkOS SSO + Directory Sync Demo App – Okta + Node.js

This is a demo app built in Node.js to test both:
- SAML-based Single Sign-On (SSO)
- Directory Sync (SCIM) integration

WorkOS acts as the identity abstraction layer and Okta is used as both the Identity Provider (IdP) and Directory provider.

---

## Technologies Used

- Node.js
- Express.js
- WorkOS Node SDK
- EJS templates
- Okta (SAML IdP + Directory Sync)
- HTML/CSS

---

## Prerequisites

1. Node.js v22+ installed locally
2. A [WorkOS](https://workos.com) account
3. A [Okta](https://developer.okta.com/signup/) account
4. Git

---

## Local Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/pandresss/workos-sso-demoapp-ps.git
cd workos-sso-demoapp-ps
```

### 2. Install Dependencies

```bash
npm install
```
check versions to ensure proper installion

```bash
npm -v
```


### 3. Create a `.env` File

Create a `.env` file in the root of the project (`node-sso-example/`) and add the following:

```env
WORKOS_API_KEY=sk_test_...
WORKOS_CLIENT_ID=client_...
PORT=3000
```

Use actual values from your [WorkOS Dashboard](https://dashboard.workos.com/).

### 4. Start the Server

```bash
npm start
```

Visit: [http://localhost:3000](http://localhost:3000)

---

## Setting up SAML SSO via WorkOS

### 1. In WorkOS:
- Go to your [WorkOS dashboard](https://dashboard.workos.com/organizations).
- Create a new Organization.
- Note the Organization ID (e.g., `org_...`).

### 2. Create a SAML Connection
- Under the Organization, add a connection.
- Choose **SAML** → Select **Okta**.
- Upload the metadata XML file from Okta (below).

### 3. In Okta:
- Create a new App Integration → SAML 2.0.
- Set:
  - **Single Sign-On URL**: `http://localhost:3000/callback`
  - **Audience URI (SP Entity ID)**: Your WorkOS Client ID.
- Download the metadata XML and upload it to WorkOS.

### 4. Assign Users
- In Okta, assign test users to the app with matching email domains (e.g., `user@yourcompany.com`).

---

## Enable Directory Sync 

Directory Sync lets you fetch and view users in your Okta directory through WorkOS.

### 1. In WorkOS:
- Navigate to [Directory Sync](https://dashboard.workos.com/directory-sync).
- Click **+ Create Directory** → Choose **Okta**.
- Note the Directory ID (e.g., `directory_...`).
- You’ll receive a **SCIM Base URL** and **Bearer Token**.

### 2. In Okta:
- Go to **Applications** → Create App Integration → **SCIM**.
- Enter:
  - SCIM Connector Base URL: from WorkOS
  - Bearer Token: from WorkOS
- Enable:
  - **Push Users**
  - **Push Groups** (optional)
- Assign users to the SCIM app.
- Users will begin syncing to WorkOS.

### 3. In the App:
- Once synced, visit [http://localhost:3000/directory-users](http://localhost:3000/directory-users) to view directory users.

More info: [WorkOS Directory Sync Docs](https://docs.workos.com/directory-sync/overview)

---

## App Features

- Login page with SSO buttons for SAML, Google, and Microsoft OAuth.
- Successful login redirects to profile details view.
- Directory Sync users shown on a separate `/directory-users` page.
- Navigation buttons added to move between views.

---

## Troubleshooting issues I faced. 

- `connection_invalid` – Confirm the Connection ID matches the one from WorkOS.
- `profile_not_allowed_outside_organization` – User’s email domain must match the WorkOS organization domain.
- Port errors – Ensure nothing else is using port 3000.
- Directory users not showing – Ensure SCIM provisioning is active in Okta.

---
