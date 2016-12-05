FROM senasi/php:7.0

RUN wget https://getcomposer.org/installer -O - -q | php -- --install-dir=/usr/bin --filename=composer

RUN apk --no-cache add \
        git \
        openssh \
        perl

RUN mkdir /data
VOLUME /data
WORKDIR /data

ENV COMPOSER_ALLOW_SUPERUSER=1

ENTRYPOINT ["composer"]
CMD ["update"]
