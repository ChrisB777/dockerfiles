FROM alpine:3.2
MAINTAINER xataz <https://github.com/xataz/>

ENV JAVA_HOME=/opt/jre \
    JAVA_VERSION=8u74-b02 \
    FOLDER_TMP=jre1.8.0_74 \
    GLIBC_URL=https://github.com/andyshinn/alpine-pkg-glibc/releases/download/unreleased \
    GLIBC_VER=2.23-r1

RUN export BUILD_DEPS="wget \
			ca-certificates" \
    && apk add -U ${BUILD_DEPS} \
    && wget --no-check-certificate ${GLIBC_URL}/glibc-${GLIBC_VER}.apk -O /tmp/glibc-${GLIBC_VER}.apk \
    && wget --no-check-certificate ${GLIBC_URL}/glibc-bin-${GLIBC_VER}.apk -O /tmp/glibc-bin-${GLIBC_VER}.apk \
    && apk add --allow-untrusted /tmp/glibc-${GLIBC_VER}.apk \
                                    /tmp/glibc-bin-${GLIBC_VER}.apk \
    && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf \
    && mkdir /opt \
    && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
	http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}/jre-$(echo ${JAVA_VERSION} | cut -d- -f1)-linux-x64.tar.gz -O /tmp/jre.tgz \
    && cd /opt \
    && tar zxvf /tmp/jre.tgz \
    && mv ${FOLDER_TMP} jre \
    && ln -s /opt/jre/bin/java /usr/bin/java \
    && cd /opt/jre/lib/amd64 \
    && rm libjavafx_* libjfx* libfx* \
    && cd /opt/jre/lib/ \
    && rm -rf ext/jfxrt.jar jfxswt.jar javafx.properties font* \
    && apk del ${BUILD_DEPS} \
    && rm /tmp/* /var/cache/apk/*

ENV FB_VER=4.6.1

RUN apk add -U wget \
                unzip \
    && mkdir /opt/filebot \
    && cd /opt/filebot \
    && wget http://downloads.sourceforge.net/project/filebot/filebot/FileBot_${FB_VER}/FileBot_${FB_VER}-portable.zip \
    && unzip FileBot_${FB_VER}-portable.zip \
    && chmod -R 777 /opt/filebot \
    && apk del wget \
                unzip \
    && rm -rf /opt/filebot/FileBot_${FB_VER}-portable.zip /var/cache/apk/*

ENV DELUGE_VER=1.3-stable UID=991 GID=991

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
	apk add --update bash python build-base python-dev py-setuptools py-six py-mako py-chardet \
		xdg-utils py-gtk libtorrent-rasterbar@testing py-openssl \
		py-twisted py-enum34 openssl-dev py-pip librsvg libffi-dev git supervisor && \
	pip install service_identity pyxdg cffi cryptography && \
	cd / && git clone -b ${DELUGE_VER} https://github.com/deluge-torrent/deluge.git && \
	cd /deluge && python setup.py build && python setup.py install && \
	apk del py-pip git build-base libffi-dev openssl-dev python-dev && rm -rf /var/cache/apk/* /deluge

EXPOSE 53160 53160/udp 8112 58846

VOLUME ["/data", "/config"]

ENV PUSHBULLET_APIKEY=""
	TVSHOW_FORMAT="TVShow/{n}/{'Saison '+s}/{n} - {sxe} - {t}"
	MOVIES_FORMAT="Movies/{n} ({y}) by {director} [{genres[0]}]"
	WEB_ROOT=/
ADD rootfs /

RUN chmod +x /usr/bin/startup && chmod +x /config/postdl && chmod +x /config/postrm && cp -r /config /config-bck

CMD ["/usr/bin/startup"]
