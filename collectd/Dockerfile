FROM debian:jessie-slim

MAINTAINER Development Team <dev@facette.io>

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "deb http://deb.debian.org/debian/ jessie-backports main" >>/etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends -t jessie-backports \
        collectd \
        ca-certificates \
        libcurl3-gnutls \
        libyajl2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY collectd.conf /etc/collectd/collectd.conf

ENTRYPOINT ["collectd", "-f", "-C", "/etc/collectd/collectd.conf"]

# vim: ts=4 sw=4 et
