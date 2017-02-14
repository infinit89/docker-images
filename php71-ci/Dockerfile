FROM php:7.1

MAINTAINER Miguel González <infinit89@gmail.com>

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yqq \
    curl \
    git \
    zip \
    unzip \
    zlib1g-dev \
    libicu-dev \
    libbz2-dev \
    libmcrypt-dev \
    libsqlite3-dev \
    libsqlite3-0 \
    libpq-dev \
    php-pear \
    g++ \
    nodejs \
    npm \
  && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-install mcrypt zip bz2 mbstring pdo_mysql pdo_pgsql pdo_sqlite intl 

# PHP xdebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# NPM Extensions
RUN npm install -g bower

# Memory Limit and Time Zone
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "date.timezone=Europe/Madrid" > $PHP_INI_DIR/conf.d/date_timezone.ini

ENV COMPOSER_ALLOW_SUPERUSER 1

# Install composer and dependencies for this build
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN php --version
RUN composer --version