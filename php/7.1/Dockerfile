FROM php:7.1-fpm-alpine

RUN apk add --no-cache --virtual .run-deps \
        openssl \
        libmcrypt \
        zlib \
        libxslt \
        libxml2 \
        freetype \
        libwebp \
        libjpeg \
        libpng && \
    apk add --no-cache --virtual .build-deps \
        openssl-dev \
        libmcrypt-dev \
        zlib-dev  \
        libxslt-dev \
        libxml2-dev \
        freetype-dev \
        libwebp-dev \
        libjpeg-turbo-dev \
        libpng-dev && \
    docker-php-ext-configure gd  --with-jpeg-dir=/usr/include/ --with-freetype-dir=/usr/include/ --with-webp-dir=/usr/include/ && \
    pecl install mongodb mailparse && \
    docker-php-ext-enable mongodb mailparse && \
    docker-php-ext-install calendar gd pcntl pdo_mysql soap sockets xsl zip opcache mcrypt && \
    apk del .build-deps
