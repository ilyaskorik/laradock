FROM nginx:alpine

MAINTAINER Mahmoud Zalt <mahmoud@zalt.me>

ADD nginx.conf /etc/nginx/

ARG PHP_UPSTREAM_71=php-fpm
ARG PHP_UPSTREAM_70=php-fpm-old

# fix a problem--#397, change application source from dl-cdn.alpinelinux.org to aliyun source.
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data \
    && rm /etc/nginx/conf.d/default.conf \
    && echo "upstream php-upstream-71 { server ${PHP_UPSTREAM_71}:9000; }" > /etc/nginx/conf.d/upstream.conf \
    && echo "upstream php-upstream-70 { server ${PHP_UPSTREAM_70}:9000; }" >> /etc/nginx/conf.d/upstream.conf

CMD ["nginx"]

EXPOSE 80 443
