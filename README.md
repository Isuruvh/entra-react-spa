# React SPA - Microsoft Entra External ID sign-in sample

A small React single-page application (SPA) for trying the Microsoft Entra External ID sign-in flow. It uses the Microsoft Authentication Library for React (MSAL React) and the MSAL browser library.

After signing in, the app displays claims from the user's ID token. The sample uses redirect-based authentication and includes sign-in, sign-up, and sign-out controls.

## Requirements

- Node.js and npm
- A Microsoft Entra External ID tenant
- An app registration in that tenant configured as a single-page application

## Configure the app registration

In your Entra External ID tenant, register a SPA and add the URL where you will run the app as a **Single-page application** redirect URI. For local development, use:

```text
http://localhost:3000
```

Add the redirect URI for each environment where you plan to run the app. A client secret is not needed for a browser-based SPA.

## Configure this sample

Update the MSAL settings in [`src/authConfig.js`](./src/authConfig.js) to match your app registration and tenant:

- `clientId`: the Application (client) ID of your app registration.
- `authority`: your External ID tenant's sign-in authority.
- `knownAuthorities`: the host name for that authority.
- `loginRequest.scopes`: the scopes to request, if you add API access. The sample currently relies on MSAL's default OpenID Connect scopes.

The current file contains sample tenant values. Replace them with the values for your own tenant before using this sample with another registration.

## Run locally

Install dependencies and start the development server:

```bash
npm install
npm start
```

Open [http://localhost:3000](http://localhost:3000). Choose **Sign up** to start the sign-up redirect flow. After returning to the app, the ID-token claims are shown. The navigation bar also provides sign-in and sign-out controls.

## Available scripts

| Command | Description |
| --- | --- |
| `npm start` | Start the local development server. |
| `npm test` | Run the tests in interactive watch mode. |
| `npm run build` | Create an optimized production build in the `build` directory. |

## Project structure

- `src/authConfig.js` — MSAL authority, app registration, and login scopes.
- `src/index.js` — Creates the MSAL `PublicClientApplication` and mounts the React app.
- `src/App.js` — Provides the MSAL context and renders sign-in/sign-up or authenticated content.
- `src/components/` — Navigation, page layout, and ID-token claim display.

## Troubleshooting

- If sign-in fails or returns to an error page, check that the tenant authority and `knownAuthorities` match your External ID tenant.
- Confirm the app registration includes the exact redirect URI, including scheme, host, port, and path.
- If you change the local port or use a deployed URL, register that URL as a SPA redirect URI and use it to open the app.
