
FROM php:7.2-apache


# Install mysql
RUN apt-get update \
  && apt-get install -y mysql-client \
  && docker-php-ext-install pdo pdo_mysql mysqli

# Install gd
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

COPY ../../php/php72/config/php.ini /usr/local/etc/php/
COPY config/vhost.conf /etc/apache2/sites-enabled/vhost.conf

# Expose the port
EXPOSE 80