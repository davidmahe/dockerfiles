# Stage 1:  
# - Get Shaarli sources  
# - Resolve PHP dependencies with Composer  
FROM composer:latest as composer  
RUN curl -L https://github.com/shaarli/Shaarli/archive/latest.tar.gz | tar xzf
- \  
&& mv Shaarli-latest shaarli \  
&& cd shaarli \  
&& composer --prefer-dist --no-dev install  
  
# Stage 2:  
# - Shaarli image  
FROM alpine:3.6  
LABEL maintainer="Shaarli Community"  
  
RUN apk --update --no-cache add \  
ca-certificates \  
nginx \  
php7 \  
php7-ctype \  
php7-curl \  
php7-fpm \  
php7-gd \  
php7-iconv \  
php7-intl \  
php7-json \  
php7-mbstring \  
php7-openssl \  
php7-session \  
php7-xml \  
php7-zlib \  
s6  
  
COPY nginx.conf /etc/nginx/nginx.conf  
COPY php-fpm.conf /etc/php7/php-fpm.conf  
COPY services.d /etc/services.d  
  
RUN rm -rf /etc/php7/php-fpm.d/www.conf \  
&& sed -i 's/post_max_size.*/post_max_size = 10M/' /etc/php7/php.ini \  
&& sed -i 's/upload_max_filesize.*/upload_max_filesize = 10M/'
/etc/php7/php.ini  
  
WORKDIR /var/www  
COPY \--from=composer /app/shaarli shaarli  
  
RUN chown -R nginx:nginx . \  
&& ln -sf /dev/stdout /var/log/nginx/shaarli.access.log \  
&& ln -sf /dev/stderr /var/log/nginx/shaarli.error.log  
  
VOLUME /var/www/shaarli/data  
  
EXPOSE 80  
ENTRYPOINT ["/bin/s6-svscan", "/etc/services.d"]  
CMD []  

