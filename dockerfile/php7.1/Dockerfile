FROM php:7.1-fpm

COPY conf/sources.list /etc/apt/sources.list

ADD https://mirrors.aliyun.com/composer/composer.phar /usr/local/bin/composer

RUN set -xe \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd pdo_mysql zip mysqli bcmath pcntl exif \
    && pecl install -o -f redis-5.0.2 \
    && docker-php-ext-enable redis \
    && chmod a+x /usr/local/bin/composer \
    && rm -rf /tmp/pear \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app