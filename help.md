```markdown
# Keycloak OpenID Connect Example Requests

This document provides example `curl` requests for various OpenID Connect (OIDC) endpoints in Keycloak. Replace the placeholder values (e.g., `CLIENT_ID`, `CLIENT_SECRET`, `USERNAME`, `PASSWORD`) with your actual values.

## 1. Authorization Endpoint

This is where you request authorization from the user.

### Request:
```bash
curl -X GET "http://localhost:9080/realms/master/protocol/openid-connect/auth?client_id=CLIENT_ID&response_type=code&scope=openid&redirect_uri=http://localhost:8080/callback"
```

### Parameters:
- `client_id`: Your client ID registered in Keycloak.
- `response_type`: Use `code` for authorization code flow.
- `scope`: Specify the scope (`openid` is mandatory for OpenID Connect).
- `redirect_uri`: The URI where the user will be redirected after authorization.

## 2. Token Endpoint

Exchange the authorization code for an access token.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/token" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "grant_type=authorization_code" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET" \
    -d "code=AUTHORIZATION_CODE" \
    -d "redirect_uri=http://localhost:8080/callback"
```

### Parameters:
- `grant_type`: Use `authorization_code` for this flow.
- `client_id`: Your client ID.
- `client_secret`: Your client secret (if your client is confidential).
- `code`: The authorization code received from the authorization endpoint.
- `redirect_uri`: Same URI as used in the authorization request.

## 3. Refresh Token

To refresh the access token when it expires, use the refresh token.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/token" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "grant_type=refresh_token" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET" \
    -d "refresh_token=REFRESH_TOKEN"
```

### Parameters:
- `grant_type`: Use `refresh_token`.
- `refresh_token`: The refresh token obtained from the initial token request.

## 4. User Info Endpoint

Retrieve user information from the access token.

### Request:
```bash
curl -X GET "http://localhost:9080/realms/master/protocol/openid-connect/userinfo" \
    -H "Authorization: Bearer ACCESS_TOKEN"
```

### Parameters:
- `Authorization`: Add the access token as a Bearer token in the request header.

## 5. Introspection Endpoint

Use this to validate the token (requires client credentials).

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/token/introspect" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "token=ACCESS_TOKEN" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET"
```

### Parameters:
- `token`: The token to introspect (validate).
- `client_id`: Your client ID.
- `client_secret`: Your client secret.

## 6. Logout Endpoint

To log out a user and invalidate their session.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/logout" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET" \
    -d "refresh_token=REFRESH_TOKEN"
```

### Parameters:
- `refresh_token`: The refresh token of the session to be invalidated.

## 7. Token Revocation

Revoke a token to prevent further use.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/revoke" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "token=ACCESS_OR_REFRESH_TOKEN" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET"
```

### Parameters:
- `token`: The token you wish to revoke.
- `client_id`: Your client ID.
- `client_secret`: Your client secret.

## 8. JWKS (JSON Web Key Set)

To get the public keys for verifying tokens.

### Request:
```bash
curl -X GET "http://localhost:9080/realms/master/protocol/openid-connect/certs"
```

## 9. Device Authorization Endpoint

Initiate device flow to authorize a device.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/auth/device" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "client_id=CLIENT_ID" \
    -d "scope=openid"
```

### Parameters:
- `client_id`: Your client ID.
- `scope`: Specify the scope (e.g., `openid`).

## 10. Token Revocation Endpoint

Revoke tokens to prevent further access.

### Request:
```bash
curl -X POST "http://localhost:9080/realms/master/protocol/openid-connect/revoke" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -d "client_id=CLIENT_ID" \
    -d "client_secret=CLIENT_SECRET" \
    -d "token=REFRESH_TOKEN"
```

---

