FROM php:7.4-apache

ENV COMPOSER_ALLOW_SUPERUSER=1

# PHP Extensions
RUN docker-php-ext-install opcache pdo_mysql
# Use the default production configuration
RUN mv $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini
COPY ./docker/conf/php.ini /usr/local/etc/php/conf.d/app.ini


COPY ./docker/conf/vhost.conf /etc/apache2/sites-available/vhost.conf
COPY ./docker/conf/apache.conf /etc/apache2/conf-available/app.conf
RUN a2ensite vhost.conf
RUN a2enmod rewrite remoteip && \
    a2enconf app

COPY . /var/www/html/app
RUN chown  -R www-data:www-data /var/www/html/app


WORKDIR /var/www/html/app

# Expose ports
EXPOSE 80
EXPOSE 443