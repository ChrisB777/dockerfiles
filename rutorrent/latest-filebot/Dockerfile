FROM xataz/rutorrent
MAINTAINER xataz <https://github.com/xataz>

ENV UID=991 \
    GID=991 \
    FILEBOT_VER=4.6.1 \
    WEBROOT=/ \
    PORT_RTORRENT=45000

RUN apk add -U openjdk8-jre \
    && mkdir /filebot \
    && cd /filebot \
    && wget http://downloads.sourceforge.net/project/filebot/filebot/FileBot_${FILEBOT_VER}/FileBot_${FILEBOT_VER}-portable.zip \
    && unzip FileBot_${FILEBOT_VER}-portable.zip \
    && apk del ${BUILD_DEPS} \
    && rm -rf /var/cache/apk/* /tmp/* /FileBot_${FILEBOT_VER}-portable.zip

ADD rootfs /
VOLUME /data
EXPOSE 8080
RUN chmod +x /usr/bin/startup
RUN chmod +x /usr/bin/postdl
RUN chmod +x /usr/bin/postrm

CMD ["tini","--","startup"]
