FROM php:7.2-apache

ENV APT_DEPS \
        zip \
        unzip
RUN set -eux; \
        apt-get update; \
        apt-get install -y --no-install-recommends ${APT_DEPS}; \
        rm -rf /var/lib/apt/lists/*

ENV PHP_EXT_INSTALL \
        bcmath \
        pdo_mysql \
        opcache
RUN docker-php-ext-install ${PHP_EXT_INSTALL}

COPY opcache.ini ${PHP_INI_DIR}/conf.d/opcache.ini
COPY vhost.conf ${APACHE_CONFDIR}/sites-available/000-default.conf

RUN curl -fsSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN a2enmod rewrite
