# From official php image.
FROM php:cli

RUN addgroup --gid 1000 user && adduser --uid 1000 --gid 1000 user
RUN apt update -y && apt install -y zip git libpq-dev && apt clean
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - && \
    apt-get install -y nodejs
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

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

RUN npm i -g yarn
# Prevent container from exiting early.
CMD ["sleep", "infinity"]
