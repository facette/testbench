FROM debian:stretch-slim

LABEL maintainer="Facette Developers <dev@facette.io>"

ARG KAIROSDB_VERSION

ARG KAIROS_CARBON_VERSION

ENV DEBIAN_FRONTEND=noninteractive

RUN mkdir -p /usr/share/man/man1 && \
    echo "deb http://deb.debian.org/debian/ stretch-backports main" >>/etc/apt/sources.list && \
    apt-get update && \
    apt-get install --no-install-recommends -t stretch-backports -y \
        ca-certificates \
        curl \
        openjdk-8-jre-headless && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -s -L -O https://github.com/kairosdb/kairosdb/releases/download/v${KAIROSDB_VERSION}/kairosdb_${KAIROSDB_VERSION}-1_all.deb && \
    curl -s -L -O https://github.com/kairosdb/kairos-carbon/releases/download/v${KAIROS_CARBON_VERSION}/kairos-carbon_${KAIROS_CARBON_VERSION}-1_all.deb && \
    dpkg -i kairosdb_${KAIROSDB_VERSION}-1_all.deb kairos-carbon_${KAIROS_CARBON_VERSION}-1_all.deb && \
    rm -rf /tmp/*

COPY kairosdb.properties kairos-carbon.properties /opt/kairosdb/conf/

RUN chown -R nobody:nogroup /opt/kairosdb

USER nobody:nogroup

EXPOSE 2003 8080

WORKDIR /opt/kairosdb

ENTRYPOINT [ "/opt/kairosdb/bin/kairosdb.sh" ]

CMD [ "run" ]

# vim: ts=4 sw=4 et
