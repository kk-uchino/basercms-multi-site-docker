FROM php:7.4-fpm

RUN apt update && \
    apt install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev

RUN docker-php-ext-install \
    pdo_mysql \
    gd \
    zip

RUN pecl install xdebug-3.1.6 && \
    docker-php-ext-enable xdebug
