FROM ubuntu:16.04  
  
MAINTAINER Pterodactyl Software, <support@pterodactyl.io>  
ENV DEBIAN_FRONTEND noninteractive  
# Install Dependencies  
RUN dpkg --add-architecture i386 \  
&& apt-get update \  
&& apt-get upgrade -y \  
&& apt-get install -y tar curl gcc g++ lib32gcc1 lib32tinfo5 lib32z1
lib32stdc++6 libtinfo5:i386 libncurses5:i386 libcurl3-gnutls:i386 gdb lsof \  
&& useradd -m -d /home/container container \  
&& mkdir -p /tmp/dumps && chmod -R 777 /tmp/ \  
&& chown root:root /tmp/dumps  
  
  
USER  container  
ENV HOME /home/container  
WORKDIR /home/container  
  
COPY ./entrypoint.sh /entrypoint.sh  
CMD ["/bin/bash", "/entrypoint.sh"]  

