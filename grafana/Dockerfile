# syntax=docker/dockerfile:1

ARG GRAFANA_VERSION=11.6.0

# Stage 1: 
FROM alpine:3.21 AS provisioning
COPY provisioning /etc/grafana/provisioning
RUN test -f /etc/grafana/provisioning/datasources/prometheus.yml

# Stage 2
FROM grafana/grafana-oss:${GRAFANA_VERSION}
USER root
COPY --from=provisioning /etc/grafana/provisioning /etc/grafana/provisioning
RUN chown -R grafana:root /etc/grafana/provisioning
USER grafana
