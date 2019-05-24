FROM nediiii/alpine

LABEL maintainer="nediiii <varnediiii@gmail.com>"

# install openjdk8
RUN apk add --no-cache openjdk8

ENV JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk" \
    PATH="$PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin"

# docker build . -t nediiii/openjdk8
