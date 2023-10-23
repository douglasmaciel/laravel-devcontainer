# From official php image.
FROM php:fpm

RUN apt update -y && apt install -y git libpq-dev && apt clean
RUN docker-php-ext-install \
    bcmath \
    ctype \
    pdo \
    pdo_pgsql \
    pdo_mysql \
    && pecl install redis

RUN docker-php-ext-enable \
    bcmath \
    ctype \
    pdo \
    pdo_pgsql \
    pdo_mysql \
    redis
