FROM php:5.6-fpm

RUN echo "deb http://archive.debian.org/debian/ stretch main" > /etc/apt/sources.list && \
    echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list

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

RUN pecl install xdebug-2.5.5 && \
    docker-php-ext-enable xdebug
