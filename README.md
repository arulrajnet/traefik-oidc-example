# Traefik OIDC Example

This is a simple example demonstrating how to use Traefik with OIDC authentication using the `traefik-oidc` plugin.

## Features

- **Traefik Proxy**: Traefik with SSL self-signed certificates.
- **OIDC Authentication**: Using the `github.com/lukaszraczylo/traefikoidc` plugin
- **Whoami Service**: Simple upstream service protected by OIDC authentication
- **Environment Configuration**: All OIDC settings loaded from `.env` file

## Architecture

![Traefik with OIDC Plugin](./traefik-oidc-plugin.drawio.svg)

## Setup Instructions

### 1. Configure OIDC Provider

Edit the `.env` file and replace the placeholder values with your actual OIDC provider details:

```bash
# Example for Auth0
OIDC_PROVIDER_URL=https://your-tenant.auth0.com
OIDC_CLIENT_ID=your-auth0-client-id
OIDC_CLIENT_SECRET=your-auth0-client-secret

# Example for Keycloak
OIDC_PROVIDER_URL=https://your-keycloak.com/auth/realms/your-realm
OIDC_CLIENT_ID=your-keycloak-client-id
OIDC_CLIENT_SECRET=your-keycloak-client-secret

# Example for Google
OIDC_PROVIDER_URL=https://accounts.google.com
OIDC_CLIENT_ID=your-google-client-id.apps.googleusercontent.com
OIDC_CLIENT_SECRET=your-google-client-secret
```

### 2. Configure Redirect URIs

In your OIDC provider settings, make sure to configure the following redirect URIs:
- `https://localhost/oauth2/callback`
- `https://localhost/oauth2/logout`

### 3. Generate Session Encryption Key

Generate a 32-character encryption key for session encryption:

```bash
openssl rand -hex 16
```

Update the `OIDC_SESSION_ENCRYPTION_KEY` in your `.env` file with this value.

### 4. Start the Services

```bash
docker-compose up -d
```

### 5. Access the Application

1. Open your browser and navigate to `https://localhost/`
2. You will be redirected to your OIDC provider for authentication
3. After successful login, you'll be redirected back and see the whoami service response

## Endpoints

- **Application**: `https://localhost/` (protected by OIDC)
- **OIDC Callback**: `https://localhost/oauth2/callback`
- **Logout**: `https://localhost/oauth2/logout`

## Plugin Configuration

The [OIDC plugin](https://github.com/lukaszraczylo/traefikoidc) supports various configuration options:

- `providerURL`: Your OIDC provider URL
- `clientID`: Your OIDC client ID
- `clientSecret`: Your OIDC client secret
- `callbackURL`: OAuth2 callback path
- `logoutURL`: OAuth2 logout path
- `postLogoutRedirectURI`: Where to redirect after logout
- `sessionEncryptionKey`: Key for encrypting session data
- `scopes`: OIDC scopes to request
- `forceHTTPS`: Force HTTPS for secure communication

## Cleanup

To stop and remove all containers:

```bash
docker-compose down -v
```

## Author

<p align="center">
  <a href="https://x.com/arulrajnet">
    <img src="https://github.com/arulrajnet.png?size=100" alt="Arulraj V" width="100" height="100" style="border-radius: 50%;" class="avatar-user">
  </a>
  <br>
  <strong>Arul</strong>
  <br>
  <a href="https://x.com/arulrajnet">
    <img src="https://img.shields.io/badge/Follow-%40arulrajnet-1DA1F2?style=for-the-badge&logo=x&logoColor=white" alt="Follow @arulrajnet on X">
  </a>
  <a href="https://github.com/arulrajnet">
    <img src="https://img.shields.io/badge/GitHub-arulrajnet-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub @arulrajnet">
  </a>
  <a href="https://linkedin.com/in/arulrajnet">
    <img src="https://custom-icon-badges.demolab.com/badge/LinkedIn-arulrajnet-0A66C2?style=for-the-badge&logo=linkedin-white&logoColor=white" alt="LinkedIn @arulrajnet">
  </a>
</p>
