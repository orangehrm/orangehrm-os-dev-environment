FROM php:7.4-fpm

COPY config/php.ini /usr/local/etc/php/
COPY files/ioncube_loader_lin_7.4_10.4.0_beta2.so /usr/local/lib/php/extensions/

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
	# https://github.com/docker-library/php/issues/912
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-configure ldap --with-libdir=lib/$(uname -m)-linux-gnu/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY --from=node:12.22.7 /usr/local/bin/node /usr/bin/node

ENV YARN_VERSION 1.22.15
COPY --from=node:12.22.7 /opt/yarn-v$YARN_VERSION/ /opt/yarn-v$YARN_VERSION/
RUN ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
	&& node --version \
	&& yarn --version

RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
