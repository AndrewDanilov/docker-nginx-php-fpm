FROM php:7.4-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    git \
    zip \
    unzip \
    # php-mbstring dependencies
    libonig-dev \
    # php-xml dependencies
    libxml2-dev \
    # php-gd dependencies
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libfreetype-dev \
    libgd-dev \
    # php-zip dependencies
    libzip-dev \
    # php-intl dependencies
    libicu-dev

RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype && docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc) \
    pdo \
    pdo_mysql \
    mbstring \
    xml \
    gd \
    zip \
    intl \
    json

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www

ENTRYPOINT ["php-fpm"]
