# From official php image.
FROM php:7.4-fpm

RUN apt update -y && apt install -y git libpq-dev && apt clean
RUN docker-php-ext-install \
    bcmath \
    ctype \
    pdo \
    pdo_pgsql \
    && pecl install redis

RUN docker-php-ext-enable \
    bcmath \
    ctype \
    pdo \
    pdo_pgsql \
    redis
