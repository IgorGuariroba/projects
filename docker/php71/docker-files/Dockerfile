FROM php:7.1-fpm-alpine

RUN apk add --update --no-cache \
    vim \
    git \
    bash \
    autoconf \
    g++ \
    make \
    php71-gd \
    libzip-dev \
    libedit-dev \
    icu-dev \
    libxml2-dev \
#    libmcrypt-dev \
    freetype \
    libpng \
    libjpeg-turbo \
    freetype-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    postgresql-dev \
  &&  printf "no\n" \
   | pecl install redis-5.0.2 \
#  && printf "yes\n" \
#   | pecl install mcrypt-1.0.2 \
  && pecl install zip-1.15.5 \
  && pecl install xdebug-2.8.0 \
  && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) \
    readline \
    intl \
    soap \
    gd \
    mysqli \
    pgsql \
    bcmath \
    sockets \
    pcntl \
    pdo_mysql \
  && docker-php-ext-enable \
    redis \
 #   mcrypt \
    zip \
    xdebug

RUN set -ex \
  && apk --no-cache add \
    postgresql-dev

RUN docker-php-ext-install pdo pdo_pgsql

RUN curl -sS https://getcomposer.org/installer | \
     php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.10


COPY ./configs-php/php.ini /usr/local/etc/php/php.ini
COPY ./configs-php/www.conf /usr/local/etc/php-fpm.d/www.conf
