FROM nediiii/alpine

LABEL maintainer="nediiii <varnediiii@gmail.com>"

ENV MODE            server
ENV SERVER_ADDR     0.0.0.0
ENV SERVER_PORT     8388
ENV PASSWORD=
ENV METHOD          aes-256-gcm
ENV TIMEOUT         300
ENV DNS_ADDRS       8.8.8.8,8.8.4.4
ENV ARGS=

RUN set -ex \
     && mkdir /tmp/repo \
     && cd /tmp/repo \
     # Build environment setup
     && apk add --no-cache --virtual .build-deps \
     build-base \
     c-ares-dev \
     libev-dev \
     libsodium-dev \
     linux-headers \
     mbedtls-dev \
     pcre-dev \
     curl \
     # Get the latest releases
     && wget $(curl -s https://api.github.com/repos/shadowsocks/shadowsocks-libev/releases/latest | grep browser_download_url | cut -d '"' -f 4) \
     && tar -zxvf shadowsocks-libev* \
     && cd shadowsocks-libev* \
     # Build & install
     && ./configure --prefix=/usr --disable-documentation \
     && make install \
     && apk del .build-deps \
     # Runtime dependencies setup
     && apk add --no-cache \
     rng-tools \
     $(scanelf --needed --nobanner /usr/bin/ss-* \
     | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
     | sort -u) \
     && rm -rf /tmp/repo

CMD exec ss-$MODE \
     -s $SERVER_ADDR \
     -p $SERVER_PORT \
     -k ${PASSWORD:-$(hostname)} \
     -m $METHOD \
     -t $TIMEOUT \
     -d $DNS_ADDRS \
     -u \
     $ARGS
