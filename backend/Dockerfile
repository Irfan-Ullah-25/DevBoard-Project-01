# =========================
# BUILD STAGE
# =========================
FROM golang:1.27-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN go test ./...

RUN go build -o backend .


# =========================
# PRODUCTION STAGE
# =========================
FROM alpine:3.21

WORKDIR /app

COPY --from=builder /app/backend .

EXPOSE 5000

CMD ["./backend"]
