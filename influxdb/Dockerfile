FROM debian:jessie-slim

MAINTAINER Development Team <dev@facette.io>

ENV DEBIAN_FRONTEND=noninteractive
ENV INFLUXDB_VERSION=1.2.4

RUN echo "deb http://deb.debian.org/debian/ jessie-backports main" >>/etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends -t jessie-backports \
        ca-certificates \
        curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN cd /tmp && \
    curl -s -L -O https://dl.influxdata.com/influxdb/releases/influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    dpkg -i influxdb_${INFLUXDB_VERSION}_amd64.deb && \
    rm -rf /tmp/*

COPY influxdb.conf /etc/influxdb/influxdb.conf
COPY types.db /usr/share/collectd/types.db

EXPOSE 2003 8083 8086 25826/udp

ENTRYPOINT ["/usr/bin/influxd", "-config", "/etc/influxdb/influxdb.conf"]

# vim: ts=4 sw=4 et
