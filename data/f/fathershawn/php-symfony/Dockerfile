FROM php:7.1-fpm-alpine  
MAINTAINER digitalpulp  
  
VOLUME /var/www  
WORKDIR /var/www  
  
RUN apk add --no-cache --virtual .dd-build-deps libpng-dev libjpeg-turbo-dev
postgresql-dev libxml2-dev $PHPIZE_DEPS \  
&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \  
&& docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql zip \  
&& docker-php-ext-install opcache bcmath soap \  
&& pecl install redis xdebug ds \  
&& docker-php-ext-enable redis xdebug ds \  
&& apk add --no-cache libpng libjpeg libpq libxml2 \  
&& apk del .dd-build-deps  
  
COPY drupal-*.ini /usr/local/etc/php/conf.d/  
COPY xdebug.ini /usr/local/etc/php/conf.d/  
COPY drupal-fpm.conf /usr/local/etc/php-fpm.d  

