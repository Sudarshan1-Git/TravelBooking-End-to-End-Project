# Stage Build
FROM golang:1.26-alpine AS Builder 
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . . 
RUN CGO_ENABLED=0 go build -o search-service .


# Stage Runtime 
FROM alpine:3.23
RUN apk add --no-cache ca-certificates
WORKDIR /app
COPY --from=Builder /app/search-service .
USER 10001:10001
EXPOSE 3002
CMD ["./search-service"]
