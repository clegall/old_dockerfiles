FROM alpine:3.3
MAINTAINER Wonderfall <wonderfall@mondedie.fr>

ENV VER=6.0.beta1 GID=1000 UID=1000

RUN echo "@community http://dl-4.alpinelinux.org/alpine/v3.3/community/" >> /etc/apk/repositories \
 && apk -U add \
    ffmpeg \
    openjdk8-jre@community \
 && rm -f /var/cache/apk/*

WORKDIR /subsonic
RUN wget -qO- http://subsonic.org/download/subsonic-$VER-standalone.tar.gz | tar zxf -

COPY run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

EXPOSE 4040
VOLUME /data /musics /playlists /podcasts
CMD ["run.sh"]