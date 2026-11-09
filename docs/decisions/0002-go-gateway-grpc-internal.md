# 0002. Go gateway, gRPC inside

**Status:** accepted

## Context

Traefik already handles TLS and routing. Auth checks and the REST to gRPC translation still need a place.

## Decision

A Go gateway sits behind Traefik. It checks tokens, applies rate limits and calls internal services over gRPC. No FastAPI: Python is used only where it helps, in the ticket-generator worker.

## Consequences

- One public entry point, typed contracts inside.
- The gateway is on every request, so it must be stateless and scaled by HPA.
