# First stage: build the application
FROM golang:1.15 as builder
# Install dependencies
RUN go get github.com/codegangsta/negroni
RUN go get github.com/gorilla/mux
RUN go get github.com/xyproto/simpleredis/v2
# Copy the application code
COPY main.go .
# Build the application
RUN go build main.go
# Second stage: create the final image
FROM ubuntu:18.04
# Copy the built binary from the builder stage
COPY --from=builder /go/main /app/guestbook
# Copy the static files
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js
# Set the working directory
WORKDIR /app
# Specify the command to run the application
CMD ["./guestbook"]
# Expose port 3000
EXPOSE 3000
