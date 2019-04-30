FROM alpine

LABEL maintainer="varnediiii@gmail.com"

# speed up apk while you are in mainland china
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# set time and timezone
ENV TZ Asia/Shanghai
RUN apk update && apk add --no-cache tzdata
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["/bin/sh"]
