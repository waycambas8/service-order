FROM php:8.1-fpm

COPY .docker/extensions /builds/extensions

RUN apt-get update && apt-get install -y git \
    gcc \
    g++ \
    make autoconf

RUN apt-get install -y \
    pkg-config \
    libpq-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    unzip \
    libxml2-dev \
    libmemcached-dev \
    libmemcached11 \
    build-essential \
    libmcrypt-dev \
    libreadline-dev \
    openssl \
    libcurl4-openssl-dev \
    libssl-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-install -j$(nproc) gd \
    && mv /builds/extensions/composer.phar /usr/local/bin/composer

RUN chmod +x /usr/local/bin/composer

RUN apt-get install -y libzip-dev zlib1g-dev \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_pgsql

RUN docker-php-ext-install intl

WORKDIR /usr/share/app

RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysqli \
    dom \
    session

EXPOSE 9080 8000 80
