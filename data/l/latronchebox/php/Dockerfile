# Inherit from Heroku's stack  
FROM heroku/cedar:14  
# Internally, we arbitrarily use port 3000  
ENV PORT 3000  
# Which versions?  
ENV PHP_VERSION 5.6.15  
ENV HTTPD_VERSION 2.4.17  
ENV NGINX_VERSION 1.8.0  
# Create some needed directories  
RUN mkdir -p /app/.heroku/php /app/.profile.d  
WORKDIR /app/user  
  
# so we can run PHP in here  
ENV PATH /app/.heroku/php/bin:/app/.heroku/php/sbin:$PATH  
  
# Install Apache  
RUN curl --silent --location https://lang-php.s3.amazonaws.com/dist-
cedar-14-master/apache-$HTTPD_VERSION.tar.gz | tar xz -C /app/.heroku/php  
# Config  
RUN curl --silent --location https://raw.githubusercontent.com/heroku/heroku-
buildpack-
php/b71abaa34e36f25c33c359c5296fdd83634353d2/conf/apache2/httpd.conf.default >
/app/.heroku/php/etc/apache2/httpd.conf  
# FPM socket permissions workaround when run as root  
RUN echo "\n\  
Group root\n\  
" >> /app/.heroku/php/etc/apache2/httpd.conf  
  
# Install Nginx  
RUN curl --silent --location https://lang-php.s3.amazonaws.com/dist-
cedar-14-master/nginx-$NGINX_VERSION.tar.gz | tar xz -C /app/.heroku/php  
# Config  
RUN curl --silent --location https://raw.githubusercontent.com/heroku/heroku-
buildpack-
php/b71abaa34e36f25c33c359c5296fdd83634353d2/conf/nginx/nginx.conf.default >
/app/.heroku/php/etc/nginx/nginx.conf  
# FPM socket permissions workaround when run as root  
RUN echo "\n\  
user nobody root;\n\  
" >> /app/.heroku/php/etc/nginx/nginx.conf  
  
# Install PHP  
RUN curl --silent --location https://lang-php.s3.amazonaws.com/dist-
cedar-14-master/php-$PHP_VERSION.tar.gz | tar xz -C /app/.heroku/php  
# Config  
RUN mkdir -p /app/.heroku/php/etc/php/conf.d  
RUN curl --silent --location https://raw.githubusercontent.com/heroku/heroku-
buildpack-php/b71abaa34e36f25c33c359c5296fdd83634353d2/conf/php/php.ini >
/app/.heroku/php/etc/php/php.ini  
# Enable all optional exts  
RUN echo "\n\  
user_ini.cache_ttl = 30 \n\  
zend_extension = opcache.so \n\  
opcache.enable_cli = 1 \n\  
opcache.validate_timestamps = 1 \n\  
opcache.revalidate_freq = 0 \n\  
opcache.fast_shutdown = 0 \n\  
extension=bcmath.so \n\  
extension=calendar.so \n\  
extension=exif.so \n\  
extension=ftp.so \n\  
extension=gd.so \n\  
extension=gettext.so \n\  
extension=intl.so \n\  
extension=mbstring.so \n\  
extension=pcntl.so \n\  
extension=shmop.so \n\  
extension=soap.so \n\  
extension=sqlite3.so \n\  
extension=pdo_sqlite.so \n\  
extension=xmlrpc.so \n\  
extension=xsl.so\n\  
extension=memcached.so\n\  
memcached.use_sasl = 1\n\  
" >> /app/.heroku/php/etc/php/php.ini  
  
RUN apt-get update && apt-get install -y libmemcached  
RUN pecl install memcached  
  
# Install Composer  
RUN curl --silent --location "https://lang-php.s3.amazonaws.com/dist-
cedar-14-master/composer-1.0.0alpha11.tar.gz" | tar xz -C /app/.heroku/php  
  
# copy dep files first so Docker caches the install step if they don't change  
ONBUILD COPY composer.lock /app/user/  
ONBUILD COPY composer.json /app/user/  
# update to latest composer version  
ONBUILD RUN composer self-update  
# run install but without scripts as we don't have the app source yet  
ONBUILD RUN composer install --no-scripts --no-autoloader --ignore-plateform-
reqs  
# require the buildpack for execution  
ONBUILD RUN composer show --installed heroku/heroku-buildpack-php || { echo
'Your composer.json must have "heroku/heroku-buildpack-php" as a "require-dev"
dependency.'; exit 1; }  
# Optimize autoloader  
ONBUILD RUN composer dump-autoload --optimize  
# rest of app  
ONBUILD ADD . /app/user/  
# run install hooks  
ONBUILD RUN cat composer.json | python -c 'import sys,json; sys.exit("post-
install-cmd" not in json.load(sys.stdin).get("scripts", {}));' && composer
run-script post-install-cmd || true  
  
# TODO: run "composer compile", like Heroku?  
# ENTRYPOINT ["/usr/bin/init.sh"]  

