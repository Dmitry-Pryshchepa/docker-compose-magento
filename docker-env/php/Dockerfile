FROM php:7.2-fpm-alpine3.8

RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories
RUN apk update; \
    apk upgrade;

RUN apk add libpng-dev libjpeg-turbo-dev icu-dev libxml2-dev libxslt-dev freetype-dev

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include --with-freetype-dir=/usr/include/
RUN docker-php-ext-install mysqli gd bcmath intl mbstring pdo_mysql soap xsl zip

RUN apk add --no-cache $PHPIZE_DEPS \
    && pecl install xdebug-2.7.2 \
    && docker-php-ext-enable xdebug

# Copy xdebug settings file
COPY xdebug-custom.ini /usr/local/etc/php/conf.d/xdebug-custom.ini
