FROM debian:jessie-slim

MAINTAINER Development Team <dev@facette.io>

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "deb http://deb.debian.org/debian/ jessie-backports main" >>/etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends -t jessie-backports \
        build-essential \
        python2.7 \
        python-dev \
        python-pip \
        python-cairocffi \
        runit \
        ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install \
        django==1.9 \
        django-tagging==0.4.3 \
        scandir \
        gunicorn \
        graphite-web \
        whisper \
        carbon

COPY conf/carbon/* /opt/graphite/conf/
COPY conf/graphite-web/* /opt/graphite/webapp/graphite/
COPY service/ /etc/service/

RUN PYTHONPATH=/opt/graphite/webapp django-admin.py migrate --settings=graphite.settings --run-syncdb

EXPOSE 2003 8000

ENTRYPOINT ["runsvdir-start"]

# vim: ts=4 sw=4 et
