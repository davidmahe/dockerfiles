# Sources:  
# -https://registry.hub.docker.com/u/maxexcloo/nginx-php/dockerfile/  
# -https://github.com/maxexcloo/Docker/tree/master/frameworks/nginx-php  
  
FROM catalogomedico/nginx:latest  
MAINTAINER Edgar Gonzalez <edgar.gonzalez.catmed@gmail.com>  
RUN apt-key adv --keyserver keyserver.ubuntu.com \--recv-keys E9C74FEEA2098A6E
&& \  
echo "deb http://packages.dotdeb.org/ wheezy-php55 all" >
/etc/apt/sources.list.d/php.list && \  
apt-get update && \  
apt-get install -y php5-cli php5-curl php5-fpm php5-gd php5-mcrypt php5-mysql
php5-pgsql php5-sqlite && \  
apt-get clean && \  
echo -n > /var/lib/apt/extended_states  
RUN rm -rf /etc/nginx/addon.d /etc/php5/fpm/pool.d && \  
mkdir -p /etc/nginx/addon.d /etc/php5/fpm/pool.d  
ADD etc /etc  
ADD supervisord.conf /etc/supervisor/conf.d/php-fpm.conf  

