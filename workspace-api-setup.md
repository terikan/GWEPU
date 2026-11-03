# Workspace Tools - Google Workspace Setup

Workspace Tools connects to Google Workspace through Google's APIs using OAuth 2.0. Each organization supplies its own Google Cloud OAuth credentials.

## 1. Create a Google Cloud project

1. Open https://console.cloud.google.com/
2. Sign in with an account that can create Google Cloud projects.
3. Create a project for Workspace Tools.
4. Select the new project.

## 2. Enable the required APIs

In the Google Cloud Console, open **APIs & Services > Library** and enable:

- **Admin SDK API**
- **Chrome Management API**

## 3. Configure the OAuth application

Open **Google Auth Platform** (or the OAuth consent screen setup, depending on the Cloud Console layout).

Configure the application:

- **App name:** Workspace Tools
- **User support email:** An appropriate administrator email
- **Audience:** Internal
- **Contact information:** An administrator email

Save the configuration.

Internal is appropriate when the application will only be used by accounts in your own Google Workspace organization.

## 4. Create an OAuth client

1. Open **Google Auth Platform > Clients**.
2. Select **Create Client**.
3. Choose **Desktop app** as the application type.
4. Give it a name, such as **Workspace Tools Desktop**.
5. Create the client.

Google will display a **Client ID** and **Client Secret**. Save both values.

## 5. Configure Workspace Tools

The tool reads a file named `workspace.xml` from the same folder as `workspace.exe`.

Create or edit `workspace.xml` with the following structure:

```xml
<Settings>
    <Domain>yourdomain.org</Domain>
    <ClientID>YOUR_CLIENT_ID</ClientID>
    <secret>YOUR_CLIENT_SECRET</secret>
</Settings>
```

Replace the example values:

- `Domain`: Your Google Workspace primary domain.
- `ClientID`: The OAuth Client ID from the desktop client you created.
- `secret`: The OAuth Client Secret from that same client.

Save the file alongside `workspace.exe`.

## 6. First use and authorization

1. Launch Workspace Tools.
2. Run a function that uses the Google Workspace integration.
3. A browser window will open for Google sign-in.
4. Sign in with the Google Workspace account you intend to use.
5. Review and approve the requested permissions.

The tool requests the permissions it needs during the OAuth sign-in process. The requested permissions are defined by the application; they are not entered into `workspace.xml`.

The signed-in account must have the Google Workspace administrator privileges required for the operations being performed.

## Notes

- The tool uses a local OAuth callback at `http://127.0.0.1:43817/` during sign-in.
- The OAuth client must be created as a **Desktop app** so Google's desktop OAuth flow can be used.
- The Client ID and Client Secret belong to your organization's Google Cloud project. Keep the configuration file accessible only to people who should be able to use the integration.
