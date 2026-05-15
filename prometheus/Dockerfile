# syntax=docker/dockerfile:1

ARG PROMETHEUS_VERSION=v3.2.1

# Stage 1: validate config with promtool from upstream image
FROM prom/prometheus:${PROMETHEUS_VERSION} AS upstream

FROM upstream AS config-check
COPY prometheus.yml /etc/prometheus/prometheus.yml
RUN promtool check config /etc/prometheus/prometheus.yml

# Stage 2: runtime image with baked config
FROM prom/prometheus:${PROMETHEUS_VERSION}
COPY --from=config-check /etc/prometheus/prometheus.yml /etc/prometheus/prometheus.yml
