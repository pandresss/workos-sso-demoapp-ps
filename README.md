# Node.js Example App with SSO powered by WorkOS

An example application demonstrating how to use the [WorkOS Node.js SDK](https://github.com/workos/workos-node) to authenticate users via SSO.

## Prerequisites

Node.js version 10+

## Node.js Project Setup

1. Clone the main repo and install dependencies for the app you'd like to use:

    ```bash
    # HTTPS
    git clone https://github.com/workos/node-example-applications.git
    ```

    or

    ```bash
    # SSH
    git clone git@github.com:workos/node-example-applications.git
    ```

2. Navigate to the SSO app within the cloned repo.

    ```bash
    cd node-example-applications/node-sso-example
    ```

3. Install the dependencies.
    ```bash
    npm install
    ```

## Configure your environment

4. Grab your API Key and Client ID from your WorkOS Dashboard. Create a `.env`
   file at the project root, and store them like so:

    ```bash
    WORKOS_API_KEY=sk_xxxxxxxxxxxxx
    WORKOS_CLIENT_ID=project_xxxxxxxxxxxx
    ```

## SSO Setup with WorkOS

5. Follow the [SSO authentication flow instructions](https://workos.com/docs/sso/guide/introduction) to create a new SSO connection in your WorkOS dashboard.

6. Add `http://localhost:8000/callback` as a Redirect URI in the Configuration section of the Dashboard.

7. Update `routes/index.js` with the Organization ID.

## Testing the Integration

8. Start the server and head to http://localhost:8000/ to begin the login flow:

```sh
npm start
```

## Need help?

If you get stuck and aren't able to resolve the issue by reading our [WorkOS Node.js SDK documentation](https://docs.workos.com/sdk/node), API reference, or tutorials, you can reach out to us at support@workos.com and we'll lend a hand.



---------------------------

Paul Sanabria Addition
------------

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
