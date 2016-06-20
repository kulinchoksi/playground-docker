FROM php:7.0.3-apache

LABEL Description = "This image is used to run PHP 7, Apache and some required utilities with PHP extensions"

COPY php/php.ini /usr/local/etc/php/
COPY www/ /var/www/html/
COPY apache/sites-available/* /etc/apache2/sites-available/

RUN apt-get update && apt-get install -y \
        vim \
        zlib1g-dev \
    && docker-php-ext-install pdo_mysql zip \
    && apt-get purge --auto-remove -y zlib1g-dev \
    && apt-get clean \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && mkdir -p /var/logs/playground /var/logs/root \
    && a2enmod rewrite && a2ensite root playground && service apache2 restart

COPY docker-library/php/7.0/apache/docker-php-ext-* /usr/local/bin/
