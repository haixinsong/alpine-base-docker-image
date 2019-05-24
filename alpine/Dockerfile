FROM alpine as builder

LABEL maintainer="nediiii <varnediiii@gmail.com>"

# speed up apk while you are in mainland china
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# set time and timezone
ENV TZ Asia/Shanghai

RUN apk add --no-cache tzdata && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# ---------------------------------------------------------------------------------------------------------

FROM alpine

LABEL maintainer="varnediiii@gmail.com"

# speed up apk while you are in mainland china
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# copy timezone file to set time and timezone
COPY --from=builder /etc/localtime /etc/timezone /etc/

# CMD ["/bin/sh"]

# docker build . -t nediiii/alpine
