FROM php:7.0-fpm

COPY config/php.ini /usr/local/etc/php/
COPY files/ioncube_loader_lin_7.0.so /usr/local/lib/php/extensions/

RUN echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        apt-transport-https \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
		libxml2-dev \
		libicu-dev \
		libpq-dev \
		libldap2-dev \
		locales \
		nano \
		tzdata \
		default-mysql-client \
	&& docker-php-ext-install -j$(nproc) xmlrpc \
	    zip \
	    intl \
	    opcache \
	    pdo_pgsql \
	    pdo_mysql \
	    pgsql \
	    mysqli \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-configure ldap --with-libdir=lib/$(uname -m)-linux-gnu/ \
	&& docker-php-ext-install ldap

# Install composer globally
RUN echo "Install composer globally"

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer --version=1.10.21

RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
