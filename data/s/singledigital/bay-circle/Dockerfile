FROM php:7.1-cli  
  
ENV COMPOSER_ALLOW_SUPERUSER=1 \  
DOCKER_VERSION=17.03.2 \  
DOCKER_COMPOSE_VERSION=1.19.0 \  
HUB_VERSION=2.2.9  
# Install git  
RUN apt-get update -qq && apt-get install -qqy \  
apt-transport-https \  
ca-certificates \  
curl \  
git \  
ssh \  
zip  
  
# Install docker.  
RUN curl -L -o /tmp/docker.tgz
https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION-
ce.tgz \  
&& tar -xz -C /tmp -f /tmp/docker.tgz \  
&& mv /tmp/docker/* /usr/bin  
  
# Install docker-compose.  
RUN curl -L
https://github.com/docker/compose/releases/download/$DOCKER_COMPOSE_VERSION/docker-
compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose \  
&& chmod +x /usr/local/bin/docker-compose  
  
# Install composer.  
RUN curl -L -o /usr/local/bin/composer
https://getcomposer.org/download/1.5.2/composer.phar \  
&& echo
"61dfd2f9262a0a2469e0c1864ab1cce6d3e63f9053faf883cd08307413d92119010638bfbee7c90c9b6977e284814bcb7bfdc01dd9cb9125ac947a2968c791bc
/usr/local/bin/composer" | sha512sum \  
&& chmod +x /usr/local/bin/composer  
  
# Install composer-lock-updater  
RUN composer global require danielbachhuber/composer-lock-updater  
  
# Install hub for creating GitHub pull requests  
RUN curl -L -o /tmp/hub.tgz
https://github.com/github/hub/releases/download/v$HUB_VERSION/hub-linux-
amd64-$HUB_VERSION.tgz \  
&& tar -xz -C /tmp -f /tmp/hub.tgz \  
&& mv /tmp/hub-linux-amd64-$HUB_VERSION/bin/* /usr/bin  

