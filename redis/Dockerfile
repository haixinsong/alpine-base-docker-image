FROM nediiii/alpine

# uncomment it to speed up apk command when you are in mainland china
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache redis

EXPOSE 6379

CMD ["redis-server"]
