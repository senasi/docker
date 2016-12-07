FROM php:7.0-fpm-alpine

RUN mkdir /libiconv
COPY libiconv.patch /libiconv/
WORKDIR /libiconv

RUN apk add --no-cache --virtual .phpize-deps-configure $PHPIZE_DEPS && \
    curl -SL http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.14.tar.gz | tar -xz --strip-components=1 -C /libiconv && \
    patch -p1 -i libiconv.patch && \
    ./configure --prefix=/usr/local && \
    make && \
    make install && \
    rm -rf /libiconv && \
    apk add --no-cache --virtual .run-deps \
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

ENV LD_PRELOAD /usr/local/lib/preloadable_libiconv.so
