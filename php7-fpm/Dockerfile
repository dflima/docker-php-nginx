FROM php:7.1-fpm
ARG TIMEZONE

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
  openssl \
  git \
  unzip \
  libxml2-dev \
  libzip-dev

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s"', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini
RUN "date"

# Type docker-php-ext-install to see available options
RUN docker-php-ext-install pdo pdo_mysql soap zip

RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
