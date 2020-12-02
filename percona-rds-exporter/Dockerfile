FROM ubuntu:20.04

RUN echo "== dependencies ==" \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get upgrade -y \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        golang \
        curl \
        ca-certificates \
        git \
    && echo "done"

RUN echo "== building ==" \
    && curl -L -O https://github.com/percona/rds_exporter/archive/v0.7.0.tar.gz \
    && tar -xzf v0.7.0.tar.gz \
    && cd rds_exporter-0.7.0 \
    && go mod init github.com/percona/rds_exporter \
    && go mod vendor \
    && CGO_ENABLED=0 go build . \
    && echo "done"


FROM alpine:latest

COPY --from=0 /rds_exporter-0.7.0/rds_exporter /bin/

RUN apk update && \
    apk add ca-certificates && \
    update-ca-certificates

EXPOSE      9042
ENTRYPOINT  [ "/bin/rds_exporter", "--config.file=/etc/rds_exporter/config.yml" ]
