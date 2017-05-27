FROM debian:jessie-slim

MAINTAINER Development Team <dev@facette.io>

ENV DEBIAN_FRONTEND=noninteractive
ENV KAIROSDB_VERSION=1.1.3 KAIROS_CARBON_VERSION=1.1

RUN echo "deb http://deb.debian.org/debian/ jessie-backports main" >>/etc/apt/sources.list && \
    bash -c "mkdir -p /usr/share/man/man{1..8}" && \
    apt-get update && \
    apt-get install -y --no-install-recommends -t jessie-backports \
        openjdk-8-jre-headless \
        ca-certificates \
        curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN cd /tmp && \
    curl -s -L -O https://github.com/kairosdb/kairosdb/releases/download/v${KAIROSDB_VERSION}/kairosdb_${KAIROSDB_VERSION}-1_all.deb && \
    curl -s -L -O https://github.com/kairosdb/kairos-carbon/releases/download/v${KAIROS_CARBON_VERSION}-1/kairos-carbon_${KAIROS_CARBON_VERSION}-1_all.deb && \
    dpkg -i kairosdb_${KAIROSDB_VERSION}-1_all.deb kairos-carbon_${KAIROS_CARBON_VERSION}-1_all.deb && \
    rm -rf /tmp/*

COPY kairosdb.properties kairos-carbon.properties /opt/kairosdb/conf/

EXPOSE 2003 8080

ENTRYPOINT ["/opt/kairosdb/bin/kairosdb.sh", "run"]

# vim: ts=4 sw=4 et
