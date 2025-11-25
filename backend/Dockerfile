FROM golang:1.23-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o /app/server ./cmd/server/main.go


FROM alpine:latest

EXPOSE 8080

WORKDIR /root/

COPY --from=builder /app/server .

CMD ["./server"]