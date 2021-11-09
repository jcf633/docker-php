ARG PHP_VERSION=lastet
FROM php:${PHP_VERSION}-apache

WORKDIR /var/www/html

COPY /php-apache/apache-config/vhost.conf /etc/apache2/sites-enabled/vhost.conf

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get update && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get install -y \
    zip

RUN echo "" >> ~/.bashrc && \
    echo "# Load Custom Aliases" >> ~/.bashrc && \
    echo "source /var/www/bash-env/aliases.sh" >> ~/.bashrc && \
    echo "" >> ~/.bashrc

RUN a2enmod rewrite

EXPOSE 80 443