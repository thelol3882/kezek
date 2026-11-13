FROM golang:1.27-alpine AS builder

WORKDIR /src

COPY go.mod go.sum* ./
RUN go mod download

COPY . .

ARG VERSION=dev

RUN CGO_ENABLED=0 go build -trimpath -ldflags="-s -w -X main.version=${VERSION}" -o /out/booking .

FROM gcr.io/distroless/static-debian12:nonroot

COPY --from=builder /out/booking /booking

USER nonroot:nonroot
EXPOSE 8080

ENTRYPOINT ["/booking"]
