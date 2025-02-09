FROM php:8.4-fpm

RUN apt update && \
    apt install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libicu-dev

RUN docker-php-ext-install \
    pdo_mysql \
    gd \
    zip \
    intl

RUN pecl install xdebug && \
    docker-php-ext-enable xdebug
