FROM alpine:3.3
MAINTAINER Wonderfall <wonderfall@mondedie.fr>

ARG BRANCH=1.3-stable
ARG FB_VER=4.6.1

ENV WEBROOT=/ FB_LINK=hardlink UID=1000 GID=1000

RUN mkdir /filebot \
 && wget -q http://downloads.sourceforge.net/project/filebot/filebot/FileBot_$FB_VER/FileBot_$FB_VER-portable.zip -P /tmp \
 && unzip -q /tmp/FileBot_$FB_VER-portable.zip -d /filebot \
 && ln -s /filebot/filebot.sh /usr/local/bin/filebot \
 && rm -rf /tmp/*

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && echo "@3.2 http://nl.alpinelinux.org/alpine/v3.2/main" >> /etc/apk/repositories \
 && echo "@commuedge http://nl.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
 && echo "@community http://nl.alpinelinux.org/alpine/v3.3/community/" >> /etc/apk/repositories \
 && apk -U add \
    tar \
    ca-certificates \
    python \
    python-dev \
    libffi \
    libffi-dev \
    xdg-utils \
    py-gtk \
    openssl-dev \
    build-base \
    py-pip \
    librsvg \
    supervisor \
    boost-system@3.2 \
    boost-python@3.2 \
    libtorrent-rasterbar@testing \
    tini@commuedge \
    openjdk8-jre@community \
 && pip install --no-cache \
    service_identity \
    enum34 \
    setuptools \
    six \
    Mako \
    pyxdg \
    chardet \
    twisted \
    pyOpenSSL \
    cffi \
    cryptography \
 && cd /tmp \
 && wget -qO- https://github.com/deluge-torrent/deluge/archive/$BRANCH.tar.gz \
  | tar xz --strip 1 \
 && python setup.py build && python setup.py install \
 && apk del \
    tar \
    build-base \
    py-pip \
    libffi-dev \
    openssl-dev \
    python-dev \
    ca-certificates \
 && rm -rf /var/cache/apk/* /tmp/*

COPY fs /

RUN chmod +x /usr/local/bin/* \
 && cp -R /config /config-bkp

VOLUME /data /config
EXPOSE 53160 53160/udp 58846 8112

LABEL description "Open source, cross-platform BitTorrent client" \
      deluge "Deluge $BRANCH" \
      filebot "Filebot v$FB_VER"

CMD ["tini","--","run.sh"]
