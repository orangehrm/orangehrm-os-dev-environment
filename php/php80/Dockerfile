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
	&& docker-php-ext-configure ldap --with-libdir=lib/$(uname -m)-linux-gnu/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN pecl install xdebug && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

SHELL ["/bin/bash", "--login", "-c"]

RUN cd ~ \
	&& curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash \
	&& . $HOME/.nvm/nvm.sh \
	&& nvm install 14.18 \
	&& npm install --global yarn \
	&& node --version \
	&& yarn --version

RUN echo "${TZ}" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata
