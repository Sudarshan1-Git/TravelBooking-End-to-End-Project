#Stage Build
FROM golang:1.26-alpine AS Builder
WORKDIR /app
COPY  go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -o booking-service .

# Stage Runtime
FROM alpine:3.23 
RUN apk add --no-cache ca-certificates
COPY --from=Builder /app/booking-service . 
USER 10001:10001
EXPOSE 3003
CMD ["./booking-service"]
