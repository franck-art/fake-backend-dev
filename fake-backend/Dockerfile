# First stage:
FROM golang:1.11 as build
RUN curl -fsSL -o /usr/local/bin/dep \
  https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64 \
  && chmod +x /usr/local/bin/dep
WORKDIR /go/src/github.com/alexandrevilain/fake-backend
COPY Gopkg.toml Gopkg.lock ./
RUN dep ensure -vendor-only
COPY . ./
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

# Final stage:
FROM alpine:3.7
WORKDIR /root
COPY --from=0 /go/src/github.com/alexandrevilain/fake-backend/app .
EXPOSE 3000
CMD ["./app"] 
