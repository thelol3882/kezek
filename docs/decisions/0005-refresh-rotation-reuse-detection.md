# 0005. Rotate refresh tokens and detect reuse

**Status:** accepted

## Context

A stolen refresh token gives long-term access.

## Decision

Each refresh returns a new refresh token and marks the old one used. If a used token comes back, auth revokes the whole session chain.

## Consequences

- A stolen token works at most once before the theft is noticed.
- Both the user and the attacker have to sign in again.
