FROM php:7.4-fpm-alpine

# 基本的なあれこれとgd,node,npm,supervisor
RUN apk upgrade --update && \
    apk --no-cache --update add \
    icu-dev autoconf make g++ gcc bash git zip unzip vim\
    coreutils \
    freetype-dev \
    libjpeg-turbo-dev \
    libltdl \
    libmcrypt-dev \
    libpng-dev \
    oniguruma-dev \
    nodejs npm \
    busybox \
    supervisor

# php extension
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    bcmath opcache sockets pdo_mysql 

# install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

COPY ./app/php.ini /usr/local/etc/php/php.ini
COPY ./jobschedule/worker.conf /etc/supervisor/conf.d/worker.conf

# cron
COPY ./jobschedule/laravel-crontab /var/spool/cron/crontabs/
RUN cat /var/spool/cron/crontabs/laravel-crontab >> /var/spool/cron/crontabs/root
CMD busybox crond -f