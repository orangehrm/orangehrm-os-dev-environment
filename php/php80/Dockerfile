FROM php:8.0-fpm

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
		libldap2-dev \
		locales \
		gnupg2 \
		vim \
		git \
		cron \
		tzdata \
		default-mysql-client \
	&& docker-php-ext-install -j$(nproc) \
	    zip \
	    intl \
	    soap \
	    opcache \
	    pdo_pgsql \
	    pdo_mysql \
	    pgsql \
	    mysqli \
	    ldap \
	# https://github.com/docker-library/php/issues/912
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
	&& docker-php-ext-install -j$(nproc) gd

# Install xdebug-beta because https://bugs.xdebug.org/view.php?id=1584 issue
RUN pecl install xdebug-beta && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY --from=node:14 /usr/local/bin/node /usr/bin/node

ENV YARN_VERSION 1.22.5
COPY --from=node:14 /opt/yarn-v$YARN_VERSION/ /opt/yarn-v$YARN_VERSION/
RUN ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
	&& node --version \
	&& yarn --version


RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
