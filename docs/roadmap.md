# Roadmap

Each stage adds one new infrastructure piece and ends with a working system.

| # | Adds | Done when |
|---|---|---|
| 1 | kind cluster, PostgreSQL StatefulSet, gateway, auth, booking | a seat can't be sold twice, covered by a test |
| 2 | gRPC between services, headless Services | load spreads evenly across Pods |
| 3 | HPA, metrics-server, k6 ticket-drop scenario | a chart of replicas per service during the drop |
| 4 | Outbox and a saga with payment | an unpaid hold is released, compensation works |
| 5 | OpenTelemetry with Jaeger or Tempo | one trace across the whole saga |
| 6 | Linkerd | manual load balancing vs mesh, with numbers |
| 7 | k3s on a VPS | the same manifests run in the cloud |
