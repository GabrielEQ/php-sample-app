FROM php:7.2-apache

#Enable MysQLI  to connect to database
RUN docker-php-ext-install mysqli

WORKDIR /var/www/html/

COPY . /var/www/html/
