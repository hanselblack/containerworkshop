FROM golang:1.17 AS builder

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

ADD go.mod .
ADD go.sum .
ADD main.go .

RUN go mod download
RUN go build -o main main.go

FROM golang:1.17

ARG APP_DIR=/app

WORKDIR ${APP_DIR}

COPY --from=builder ${APP_DIR}/main .
COPY public public
COPY templates templates

# run
ENV APP_DIR=/app PORT=3000

WORKDIR ${APP_DIR}

EXPOSE ${PORT}

ENTRYPOINT [ "./main" ]