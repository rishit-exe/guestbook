FROM golang:1.20 AS builder
WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o guestbook main.go


FROM alpine:3.18
WORKDIR /app

COPY --from=builder /app/guestbook /app/guestbook
COPY public/ /app/public/

EXPOSE 3000
CMD ["./guestbook"]