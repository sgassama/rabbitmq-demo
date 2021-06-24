FROM golang:1.14-alpine as build

RUN apk add --no-cache git

WORKDIR /src

RUN go get github.com/julienschmidt/httprouter
RUN go get github.com/sirupsen/logrus
RUN go get github.com/streadway/amqp
RUN go get github.com/prometheus/client_golang/prometheus/promhttp
RUN go get github.com/prometheus/client_golang/prometheus/promauto
RUN go get github.com/prometheus/client_golang/prometheus
RUN go get github.com/gorilla/mux

COPY publisher.go /src

RUN go build publisher.go

FROM alpine as runtime

COPY --from=build /src/publisher /app/publisher

ENV RABBIT_HOST=rabbitmq-0.rabbitmq.rabbitmq-demo.svc.cluster.local
ENV RABBIT_PORT=5672
ENV RABBIT_USERNAME=guest
ENV RABBIT_PASSWORD=guest

CMD [ "/app/publisher" ]
