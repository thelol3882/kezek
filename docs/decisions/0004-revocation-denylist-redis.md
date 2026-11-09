# 0004. Revoke access tokens with a Redis denylist

**Status:** accepted

## Context

When a user ends a session or all sessions, their access tokens should stop working before they expire.

## Decision

Auth writes to Redis, the gateway only reads.

- One session: `SET revoked:sid:<sid> 1 EX <access TTL>`.
- All sessions: `SET user:<id>:revoked_before <now> EX <access TTL>`. The gateway rejects tokens with `iat` before it.
- Auth also deletes the user's refresh tokens.

A denylist, not an allowlist: an entry only has to live until the token would expire anyway, so Redis holds just the recent revocations.

If Redis is down, the gateway fails open. A revoked token then lives at most 10 more minutes.

## Consequences

- One Redis `GET` per request.
- Redis stays small and cleans itself up.
- Fail open trades a short revocation gap for availability.
