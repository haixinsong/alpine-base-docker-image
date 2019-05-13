FROM nediiii/alpine

# uncomment it to speed up apk command when you are in mainland china
# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache nginx \
    && mkdir -p /run/nginx \
    # forward request and error logs to docker log collector
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# config path
# /etc/nginx

# default html path
# /var/lib/nginx/html
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
