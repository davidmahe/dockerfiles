FROM teffcz/debian:latest  
MAINTAINER Tomas Effenberger <effik@effik.cz>  
RUN apt-key adv --keyserver keyserver.ubuntu.com \--recv-keys C2518248EEA14886
&& \  
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu/ precise main" >
/etc/apt/sources.list.d/java.list && \  
echo "debconf shared/accepted-oracle-license-v1-1 select true" | debconf-set-
selections && \  
echo "debconf shared/accepted-oracle-license-v1-1 seen true" | debconf-set-
selections && \  
apt-get update && \  
apt-get install -y oracle-java8-installer && \  
apt-get clean && \  
echo -n > /var/lib/apt/extended_states  

