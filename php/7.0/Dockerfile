FROM php:7.0-fpm-alpine

WORKDIR /build

RUN mkdir /build/libiconv && \
	mkdir /build/libsodium

COPY libiconv.patch /build/libiconv/

RUN apk add --no-cache --virtual .phpize-deps-configure $PHPIZE_DEPS && \
    cd /build/libiconv && \
    curl -SL http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.14.tar.gz | tar -xz --strip-components=1 && \
    patch -p1 -i libiconv.patch && \
    ./configure --prefix=/usr/local && \
    make && \
    make install && \
    cd /build/libsodium && \
    curl -SL https://download.libsodium.org/libsodium/releases/libsodium-1.0.12.tar.gz | tar -xz --strip-components=1 && \
    ./configure && \
    make && make check && \
    make install && \    
    rm -rf /build && \
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
    pecl install mongodb mailparse libsodium && \
    docker-php-ext-enable mongodb mailparse libsodium && \
    docker-php-ext-install calendar gd pcntl pdo_mysql soap sockets xsl zip opcache mcrypt bcmath intl && \
    apk del .build-deps

ENV LD_PRELOAD /usr/local/lib/preloadable_libiconv.so
