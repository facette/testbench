FROM facette/collectd:latest

MAINTAINER Development Team <dev@facette.io>

COPY collectd.conf /etc/collectd/collectd.conf

EXPOSE 25826/udp

ENTRYPOINT ["collectd", "-f", "-C", "/etc/collectd/collectd.conf"]

# vim: ts=4 sw=4 et
