# =========================================================
# STAGE 1: BUILDER (Lingkungan Kompilasi)
# =========================================================
FROM golang:1.22-alpine AS builder

WORKDIR /build

# Copy file dependensi dulu agar caching lebih efisien
COPY go.mod go.sum ./
RUN go mod download

# Copy kode sumber
COPY main.go ./

# Compile jadi binary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
    go build -ldflags="-s -w" -o /build/app-server main.go

# =========================================================
# STAGE 2: PRODUCTION (Lingkungan Runtime Minimalis)
# =========================================================
FROM alpine:3.20 AS production

# Install ca-certificates & wget (untuk healthcheck), lalu buat user non-root
RUN apk --no-cache add ca-certificates wget && \
    addgroup -S appgroup && \
    adduser -S -u 10001 -G appgroup appuser

WORKDIR /app

# Copy HANYA binary dari stage builder
COPY --from=builder --chown=appuser:appgroup /build/app-server /app/app-server

# Jalankan sebagai user non-root
USER appuser

EXPOSE 8080

ENTRYPOINT ["/app/app-server"]
