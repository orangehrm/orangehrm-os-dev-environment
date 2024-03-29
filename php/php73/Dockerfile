FROM php:7.3-fpm

COPY config/php.ini /usr/local/etc/php/
COPY files/ioncube_loader_lin_7.3.so /usr/local/lib/php/extensions/

RUN apt-get update && apt-get install -y \
        apt-transport-https \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
		libxml2-dev \
		libicu-dev \
		libzip-dev \
		libldap-common \
		libldap2-dev \
		locales \
		gnupg2 \
		vim \
		git \
		cron \
		tzdata \
		default-mysql-client \
	&& docker-php-ext-install -j$(nproc) xmlrpc \
	    zip \
	    intl \
	    soap \
	    opcache \
	    pdo_mysql \
	    mysqli \
	    ldap \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-configure ldap --with-libdir=lib/$(uname -m)-linux-gnu/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug-3.1.0 && docker-php-ext-enable xdebug

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
