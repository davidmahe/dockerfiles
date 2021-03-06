from ubuntu:16.04  
  
MAINTAINER Nayan V. <nayanvanza91@gmail.com>  
  
ENV DEBIAN_FRONTEND noninteractive  
  
RUN apt-get update && apt-get install -y vim \  
&& apt-get install -y software-properties-common \  
&& apt-get install -y python-software-properties \  
&& apt-get install -y apt-transport-https \  
&& apt-get install -y build-essential \  
&& apt-get install -y libreadline-gplv2-dev libncursesw5-dev libssl-dev
libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev \  
&& apt-get install -y tcl8.5 \  
&& apt-get install -y wget \  
&& apt-get install -y cron \  
&& apt-get install -y curl \  
&& apt-get install -y rsync \  
&& apt-get install -y git \  
&& apt-get install -y supervisor \  
&& apt-get install -y psmisc \  
&& apt-get install -y tree \  
&& apt-get install -y rsyslog \  
&& apt-get install -y lsb \  
&& echo "postfix postfix/mailname string root" | debconf-set-selections \  
&& echo "postfix postfix/main_mailer_type string No configuration" | debconf-
set-selections \  
&& apt-get install -y postfix mailutils libsasl2-2 libsasl2-modules \  
&& apt-get install -y openssh-server \  
&& mkdir /var/run/sshd \  
&& sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/'
/etc/ssh/sshd_config \  
&& apt-get install -y language-pack-en-base \  
&& apt-get update \  
&& locale-gen en_US.UTF-8 \  
&& export LANG=en_US.UTF-8 \  
&& LC_ALL=en_US.UTF-8 \  
&& apt-get update \  
&& cd /tmp/ \  
&& wget http://nginx.org/keys/nginx_signing.key \  
&& apt-key add nginx_signing.key \  
&& echo "deb http://nginx.org/packages/ubuntu/ xenial nginx" >>
/etc/apt/sources.list \  
&& echo "deb-src http://nginx.org/packages/ubuntu/ xenial nginx" >>
/etc/apt/sources.list \  
&& apt-get -y update \  
&& apt-get install -y nginx \  
&& apt-get install -y apache2-utils \  
&& apt-get install -y debconf-utils \  
&& cd /tmp/ \  
&& wget https://repo.percona.com/apt/percona-release_0.1-4.$(lsb_release
-sc)_all.deb \  
&& dpkg -i percona-release_0.1-4.$(lsb_release -sc)_all.deb \  
&& apt-get update \  
&& echo "percona-server-server-5.7 percona-server-server/root_password
password secret" | debconf-set-selections \  
&& echo "percona-server-server-5.7 percona-server-server/root_password_again
password secret" | debconf-set-selections \  
&& apt-get install -y percona-server-server-5.7 percona-server-client-5.7 \  
&& apt-get install -y varnish \  
&& LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php \  
&& apt-get update \  
&& apt-get install -y php7.0-fpm php7.0-mysql \  
&& apt-get install -y php7.0-cli php7.0-common php7.0-json php7.0-opcache
php7.0-gd php7.0-intl php7.0-gd php7.0-curl \  
&& apt-get install -y php7.0-mcrypt php7.0-mbstring php7.0-zip php7.0-xml
php7.0-soap php7.0-bcmath php7.0-xmlrpc \  
&& mkdir /var/run/php \  
&& cd / \  
&& wget
https://files.phpmyadmin.net/phpMyAdmin/4.6.4/phpMyAdmin-4.6.4-english.tar.gz
\  
&& tar xvzf phpMyAdmin-4.6.4-english.tar.gz \  
&& mv phpMyAdmin-4.6.4-english /phpmyadmin \  
&& rm -rf phpMyAdmin-4.6.4-english.tar.gz \  
&& cp /phpmyadmin/config.sample.inc.php /phpmyadmin/config.inc.php \  
&& add-apt-repository ppa:chris-lea/redis-server \  
&& apt-get update \  
&& apt-get -y install redis-server \  
&& apt-get update \  
&& curl -sS https://getcomposer.org/installer | php \  
&& mv composer.phar /usr/local/bin/composer \  
&& chmod +x /usr/local/bin/composer  
  
ADD tools/docker/nginx/nginx.conf /etc/nginx/nginx.conf  
ADD tools/docker/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf  
ADD tools/docker/nginx/conf.d/pma.conf /etc/nginx/conf.d/pma.conf  
ADD tools/docker/php7fpm/cli/php.ini /etc/php/7.0/cli/php.ini  
ADD tools/docker/php7fpm/fpm/php.ini /etc/php/7.0/fpm/php.ini  
ADD tools/docker/php7fpm/fpm/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf  
ADD tools/docker/php7fpm/fpm/pool.d/www.conf /etc/php/7.0/fpm/pool.d/www.conf  
ADD tools/docker/php7fpm/fpm/pool.d/pma.conf /etc/php/7.0/fpm/pool.d/pma.conf  
ADD tools/docker/postfix/main.cf /etc/postfix/main.cf  
ADD tools/docker/varnish/default.vcl /etc/varnish/default.vcl  
ADD tools/docker/varnish/varnish /etc/default/varnish  
ADD tools/docker/redis/redis.conf /etc/redis/redis.conf  
ADD tools/docker/supervisor/supervisord.conf /etc/supervisor/supervisord.conf  
ADD tools/docker/supervisor/conf.d/apps.conf /etc/supervisor/conf.d/apps.conf  
ADD tools/docker/scripts/start.sh /start.sh  
ADD tools/docker/scripts/entrypoint.sh /entrypoint.sh  
  
RUN chmod +x /*.sh  
  
EXPOSE 21 22 80 443 8080 8888 9200  
  
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]  
CMD ["/bin/bash", "/start.sh"]  

