FROM wrouesnel/postgres_exporter:v0.8.0

FROM ubuntu:18.04
COPY --from=0 /postgres_exporter /
CMD ["/postgres_exporter"]
