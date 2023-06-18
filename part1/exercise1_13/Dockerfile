FROM golang:1.16

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build

RUN go test ./... .

CMD ./server

ENV PORT=8080

ENV REQUEST_ORIGIN=https://example.com