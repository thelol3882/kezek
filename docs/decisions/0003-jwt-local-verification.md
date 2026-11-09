# 0003. Verify access tokens in the gateway

**Status:** accepted

## Context

Checking every request with the auth service makes auth a bottleneck and a single point of failure at the sale start.

## Decision

- Access token: short-lived (10 min), signed with EdDSA or RS256.
- The gateway verifies it locally with the public key from the auth JWKS endpoint, cached.
- Refresh token: long-lived, stored in `auth_db`, checked only by auth.

## Consequences

- No network call to auth on normal requests.
- Auth only takes load on login and refresh.
- A revoked token stays valid until it expires, unless the gateway checks revocation. See 0004.
