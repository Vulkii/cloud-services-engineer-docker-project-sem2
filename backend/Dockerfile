FROM golang:1.25-alpine AS builder

WORKDIR /app
COPY backend/go.mod backend/go.sum ./
RUN go mod download
COPY backend/ ./
RUN CGO_ENABLED=0 GOOS=linux go build -o backend ./cmd/api

FROM alpine:3.22
RUN apk add --no-cache ca-certificates
RUN adduser -D -g '' backenduser

COPY --from=builder /app/backend /app/backend
USER backenduser

EXPOSE 8081
ENV GIN_MODE=debug
CMD ["/app/backend"]
