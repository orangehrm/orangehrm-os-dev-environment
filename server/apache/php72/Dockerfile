
FROM php:7.2-apache


# Install mysql
RUN docker-php-source extract \
    && docker-php-ext-install pdo pdo_mysql\
    && docker-php-source delete

COPY config/php.ini /usr/local/etc/php/
COPY config/vhost.conf /etc/apache2/sites-enabled/vhost.conf

# Expose the port
EXPOSE 80