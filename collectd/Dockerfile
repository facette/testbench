FROM debian:buster-slim

LABEL maintainer="Facette Developers <dev@facette.io>"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
        collectd-core \
        libprotobuf-c1 \
        libmicrohttpd12 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY collectd.conf /etc/collectd/collectd.conf

RUN chown -R nobody:nogroup /var/lib/collectd

USER nobody:nogroup

EXPOSE 9103

VOLUME [ "/var/lib/collectd" ]

WORKDIR /var/lib/collectd

ENTRYPOINT [ "collectd" ]

CMD [ "-f", "-C", "/etc/collectd/collectd.conf" ]

# vim: ts=4 sw=4 et
