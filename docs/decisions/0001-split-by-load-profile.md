# 0001. Split services by load profile

**Status:** accepted

## Context

During a ticket drop, the load moves between parts of the system over time. A single deployment would have to scale for the peak of every part at once.

## Decision

Split services where the load profile differs: waiting-room, booking, payment, ticket-generator and the rest. Don't split by entity alone.

## Consequences

- Each service gets its own HPA and scales on its own.
- More services to deploy and observe.
- Start with gateway, auth, catalog and booking. Split further only when the load shows a reason.
