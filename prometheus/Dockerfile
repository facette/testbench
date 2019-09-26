FROM debian:buster-slim

LABEL maintainer="Facette Developers <dev@facette.io>"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
        prometheus && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY prometheus.yml /etc/prometheus/prometheus.yml

RUN chown -R nobody:nogroup /var/lib/prometheus

USER nobody:nogroup

EXPOSE 9090

VOLUME [ "/var/lib/prometheus" ]

WORKDIR /var/lib/prometheus

ENTRYPOINT [ "prometheus" ]

CMD [ "--config.file=/etc/prometheus/prometheus.yml", "--storage.tsdb.path=/var/lib/prometheus" ]

# vim: ts=4 sw=4 et
