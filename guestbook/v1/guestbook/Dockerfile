# Stage 1: Build the Go application
FROM golang:1.18 as builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Stage 2: Create the final image
FROM ubuntu:18.04

# Copy the built Go binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Copy static files (HTML, JS, CSS) to the image
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

# Set the working directory
WORKDIR /app

# Define the command to run the application
CMD ["./guestbook"]

# Expose port 3000
EXPOSE 3000
