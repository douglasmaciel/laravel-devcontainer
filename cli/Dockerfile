# From official php image.
FROM php:cli

RUN addgroup --gid 1000 user && adduser --uid 1000 --gid 1000 user
RUN apt update -y && apt install -y zip git libpq-dev && apt clean
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && \
    apt-get install -y nodejs
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

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
# Prevent container from exiting early.
CMD ["sleep", "infinity"]
