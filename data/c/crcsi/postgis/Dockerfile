#--------- Generic stuff all our Dockerfiles should start with so we get
caching ------------  
FROM debian:stable  
MAINTAINER Tim Sutton<tim@kartoza.com>  
  
RUN export DEBIAN_FRONTEND=noninteractive  
ENV DEBIAN_FRONTEND noninteractive  
RUN dpkg-divert --local \--rename --add /sbin/initctl  
#RUN ln -s /bin/true /sbin/initctl  
# Use local cached debs from host (saves your bandwidth!)  
# Change ip below to that of your apt-cacher-ng host  
# Or comment this line out if you do not with to use caching  
ADD 71-apt-cacher-ng /etc/apt/apt.conf.d/71-apt-cacher-ng  
  
#RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" >
/etc/apt/sources.list  
RUN apt-get -y update  
RUN apt-get -y install ca-certificates rpl pwgen  
  
#-------------Application Specific Stuff
----------------------------------------------------  
# We add postgis as well to prevent build errors (that we dont see on local
builds)  
# on docker hub e.g.  
# The following packages have unmet dependencies:  
# postgresql-9.3-postgis-2.1 : Depends: libgdal1h (>= 1.9.0) but it is not
going to be installed  
# Recommends: postgis but it is not going to be installed  
RUN apt-get install -y postgresql-9.4-postgis-2.1 postgis  
ADD postgres.conf /etc/supervisor/conf.d/postgres.conf  
  
# Open port 5432 so linked containers can see them  
EXPOSE 5432  
# Run any additional tasks here that are too tedious to put in  
# this dockerfile directly.  
ADD setup.sh /setup.sh  
RUN chmod 0755 /setup.sh  
RUN /setup.sh  
  
# We will run any commands in this when the container starts  
ADD start-postgis.sh /start-postgis.sh  
RUN chmod 0755 /start-postgis.sh  
  
CMD /start-postgis.sh  

