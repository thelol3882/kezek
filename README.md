# kezek

Flash-sale ticketing on Kubernetes. *Kezek* means "queue" in Kazakh.

A ticket drop sends load to different services at different times: the waiting room before the start, booking at the start, payment a few minutes later, ticket generation after that. kezek splits services by that load profile so each one scales on its own.

**Status:** design. No code yet.

## Docs

- [Architecture](docs/architecture.md)
- [Roadmap](docs/roadmap.md)
- [Decisions](docs/decisions/)

## Stack

Go, gRPC, Python, PostgreSQL, Redis, Kubernetes (kind locally, k3s in the cloud), Kustomize, k6.
