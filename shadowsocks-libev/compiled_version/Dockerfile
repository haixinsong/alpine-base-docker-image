FROM nediiii/alpine

LABEL maintainer="nediiii <varnediiii@gmail.com>"

ENV SERVER_ADDR=0.0.0.0 \
     SERVER_PORT=8388 \
     PASSWORD= \
     METHOD=aes-256-gcm \
     TIMEOUT=300 \
     DNS_ADDRS=8.8.8.8,8.8.4.4 \
     ARGS=

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
     && wget https://github.com/shadowsocks/shadowsocks-libev/releases/download/v3.3.0/shadowsocks-libev-3.3.0.tar.gz \
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

CMD exec ss-server \
     -s $SERVER_ADDR \
     -p $SERVER_PORT \
     -k ${PASSWORD:-$(hostname)} \
     -m $METHOD \
     -t $TIMEOUT \
     -d $DNS_ADDRS \
     -u \
     --fast-open \
     $ARGS

# docker build . -t nediiii/shadowsocks-libev
# test
