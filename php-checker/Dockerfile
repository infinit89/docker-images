FROM php:7

MAINTAINER Miguel González <infinit89@gmail.com>

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yqq \
    curl \
    git \
    unzip \
    zlib1g-dev \
    libicu-dev \
    libbz2-dev \
    libmcrypt-dev \
    php-pear \
    g++ \
    nodejs \
    npm \
  && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-install mcrypt zip bz2 mbstring intl

# NPM Extensions
RUN npm install -g bower

# Memory Limit and Time Zone
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "date.timezone=Europe/Madrid" > $PHP_INI_DIR/conf.d/date_timezone.ini

WORKDIR /codeanalysis

ENV COMPOSER_HOME /codeanalysis
ENV COMPOSER_ALLOW_SUPERUSER 1

# Install composer and dependencies for this build
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN cd /codeanalysis/ && composer require \
	"phpmd/phpmd" \
	"sensiolabs/security-advisories:dev-master" \
	"friendsofphp/php-cs-fixer" \
	"squizlabs/php_codesniffer" \
	"sebastian/phpcpd"

ENV PATH /codeanalysis/vendor/bin:$PATH

RUN php --version
RUN composer --version