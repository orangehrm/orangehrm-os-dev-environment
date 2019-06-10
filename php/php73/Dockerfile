FROM php:7.3-fpm

COPY config/php.ini /usr/local/etc/php/

RUN apt-get update && apt-get install -y \
        apt-transport-https \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
		libxml2-dev \
		libicu-dev \
		libpq-dev \
		libzip-dev \
		locales \
		gnupg2 \
		vim \
		git \
		cron \
	&& docker-php-ext-install -j$(nproc) xmlrpc \
	    zip \
	    intl \
	    soap \
	    opcache \
	    pdo_pgsql \
	    pdo_mysql \
	    pgsql \
	    mysqli \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

# Install xdebug-beta because https://bugs.xdebug.org/view.php?id=1584 issue
RUN pecl install xdebug-beta && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apt-get update && apt-get install -y tzdata
RUN apt install -y mysql-client

RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
