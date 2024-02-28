FROM php:8.2-fpm-alpine

# Install packages and PHP extensions
RUN docker-php-ext-install pdo mysqli pdo_mysql

# Install opcache
RUN docker-php-ext-install opcache


# Install ZIP
RUN apk add --no-cache libzip-dev
RUN docker-php-ext-install zip

# Install and update composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
RUN composer self-update

# Install some global packages
RUN apk add --no-cache bash git jq moreutils openssh rsync yq

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions
RUN install-php-extensions sockets

## Install Symfony binary
RUN apk add --no-cache bash \
    && curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.alpine.sh' | bash \
    && apk add symfony-cli

 # Copy default site conf

RUN mkdir -p /appdata/www
WORKDIR /appdata/www
