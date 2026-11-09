# 0006. One database per service, one PostgreSQL instance

**Status:** accepted

## Context

Services must not share tables, but a PostgreSQL instance per service costs too much for this scale.

## Decision

One PostgreSQL StatefulSet. Each service gets its own database and its own user with no rights on the others.

## Consequences

- Isolation is enforced by permissions, not by convention.
- The instance is a shared failure point. A service can move to its own instance later without code changes.
