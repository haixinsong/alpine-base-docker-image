# nginx alpine image

## note

If you run it without any custom-config-file,it will return 404 page whatever request in come.

## path

* nginx config path

    `/etc/nginx`

* default html path

    `/var/lib/nginx/html`

## start

```bash
docker run -d -p 80:80 \
-v /path/to/config:/etc/nginx \
-v /path/to/html:/var/lib/nginx/html \
nediiii/nginx
```
