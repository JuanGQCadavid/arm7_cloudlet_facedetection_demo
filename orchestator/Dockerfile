FROM golang:alpine3.20 as builder

ENV GOOS="linux"
ENV CGO_ENABLED="0"
ARG GOARCH="arm64"

ARG CMD="http"

WORKDIR /app

COPY cmd/${CMD} cmd/${CMD}
COPY internal internal

COPY go.mod go.mod
COPY go.sum go.sum

RUN go build -o main ./cmd/${CMD}/main.go

EXPOSE 8000

FROM alpine:3.20 as prod
COPY --from=builder /app/main /bin/
COPY internal/handler/templates internal/handler/templates
ENTRYPOINT  ["/bin/main"]

