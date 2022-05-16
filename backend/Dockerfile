FROM golang:latest AS build
WORKDIR /go/src/github.com/org/repo
COPY . .

ENV HTTPS_PROXY=http://liudhNB.lan:50000 \
    https_proxy=$HTTPS_PROXY \
    HTTP_RPOXY=$HTTPS_PROXY \
    http_proxy=$HTTPS_PROXY

ENV CGO_ENABLED=0
RUN go build -o server .

FROM build AS development
RUN apt-get update \
    && apt-get install -y git
CMD ["go", "run", "main.go"]

FROM alpine:3.12
EXPOSE 8000
COPY --from=build /go/src/github.com/org/repo/server /server
CMD ["/server"]
