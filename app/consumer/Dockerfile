FROM golang:1.14-alpine as build

RUN apk add --no-cache git

WORKDIR /src

RUN go get github.com/sirupsen/logrus
RUN go get github.com/streadway/amqp

COPY consumer.go /src

RUN go build consumer.go


FROM alpine as runtime

COPY --from=build /src/consumer /app/consumer

ENV RABBIT_HOST=rabbitmq-0.rabbitmq.rabbitmq-demo.svc.cluster.local
ENV RABBIT_PORT=5672
ENV RABBIT_USERNAME=guest
ENV RABBIT_PASSWORD=guest

CMD [ "/app/consumer" ]
