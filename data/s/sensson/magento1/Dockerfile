# Base image is PHP 5.6 running Apache  
FROM php:5.6-apache  
LABEL company="Sensson"  
LABEL maintainer="info@sensson.net"  
  
# Install Magento 1.9 dependencies  
RUN apt-get update && apt-get install -y \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libmcrypt-dev \  
libpng12-dev \  
libxml2-dev \  
libxslt1-dev \  
libicu-dev \  
mysql-client \  
xmlstarlet \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-install -j$(nproc) gd \  
&& docker-php-ext-install -j$(nproc) iconv \  
&& docker-php-ext-install -j$(nproc) mcrypt \  
&& docker-php-ext-install -j$(nproc) mbstring \  
&& docker-php-ext-install -j$(nproc) pcntl \  
&& docker-php-ext-install -j$(nproc) soap \  
&& docker-php-ext-install -j$(nproc) xsl \  
&& docker-php-ext-install -j$(nproc) zip \  
&& docker-php-ext-install -j$(nproc) intl \  
&& docker-php-ext-install -j$(nproc) pdo \  
&& docker-php-ext-install -j$(nproc) pdo_mysql \  
&& docker-php-ext-install -j$(nproc) mysqli \  
&& docker-php-ext-install -j$(nproc) mysql \  
&& pecl install redis-3.1.0 \  
&& docker-php-ext-enable redis \  
&& a2enmod rewrite headers \  
&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
# Install composer  
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
\  
&& php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \  
&& php -r "unlink('composer-setup.php');"  
  
# Install ioncube  
RUN cd /tmp \  
&& curl -o ioncube.tar.gz
http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
\  
&& tar -xvvzf ioncube.tar.gz \  
&& mv ioncube/ioncube_loader_lin_5.6.so /usr/local/lib/php/extensions/* \  
&& rm -Rf ioncube.tar.gz ioncube \  
&& echo "zend_extension=ioncube_loader_lin_5.6.so" >
/usr/local/etc/php/conf.d/00_docker-php-ext-ioncube_loader_lin_5.6.ini  
  
# Set up the application  
COPY src/ /var/www/html/  
COPY entrypoint.sh /usr/local/bin/entrypoint.sh  
COPY etc/php.ini /usr/local/etc/php/conf.d/00_magento.ini  
COPY etc/apache.conf /etc/apache2/conf-enabled/00_magento.conf  
  
# Set default parameters  
ENV MYSQL_HOSTNAME="mysql" MYSQL_USERNAME="root" MYSQL_PASSWORD="secure"
MYSQL_DATABASE="magento" CRYPT_KEY="" \  
TABLE_PREFIX="" URI="http://localhost"  
ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]  

