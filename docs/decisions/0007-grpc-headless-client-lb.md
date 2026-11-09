# 0007. Balance gRPC on the client

**Status:** accepted

## Context

gRPC keeps one long HTTP/2 connection. A normal ClusterIP Service balances connections, not requests, so all calls from one client go to one Pod even when HPA adds more.

## Decision

Use headless Services (`clusterIP: None`) for gRPC backends. Clients resolve every Pod IP over DNS and use the `round_robin` policy in grpc-go.

## Consequences

- Load spreads per request across Pods.
- Each client keeps connections to every Pod.
- Stage 6 compares this with Linkerd, which balances per request without client changes.
