FROM alpine:3.20

RUN apk add --no-cache prometheus gettext bash

WORKDIR /etc/prometheus

COPY prometheus.yml /etc/prometheus/prometheus.yml

# Prometheus가 foreground로 유지되도록 CMD로 실행
CMD bash -c 'envsubst < /etc/prometheus/prometheus.yml > /etc/prometheus/prometheus.expanded.yml && \
  exec /usr/bin/prometheus --config.file=/etc/prometheus/prometheus.expanded.yml --storage.tsdb.path=/prometheus'
