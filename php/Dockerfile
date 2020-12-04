FROM php:7.4-fpm-alpine

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
    nodejs npm

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    bcmath opcache sockets pdo_mysql 

# install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer
