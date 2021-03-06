# Use osixia/light-baseimage  
# sources: https://github.com/osixia/docker-light-baseimage  
FROM osixia/light-baseimage:0.2.1  
MAINTAINER Bertrand Gouny <bertrand.gouny@osixia.net>  
  
# Add openldap user and group first to make sure their IDs get assigned
consistently, regardless of whatever dependencies get added  
RUN groupadd -r openldap && useradd -r -g openldap openldap  
  
# Add fusiondirectory gpg key  
RUN echo "deb http://repos.fusiondirectory.org/debian-jessie jessie main" >
/etc/apt/sources.list.d/fusion.list && \  
gpg --keyserver keys.gnupg.net --recv-key 62B4981F && \  
gpg --export -a "Fusiondirectory Archive Manager
<contact@fusiondirectory.org>" > FD-archive-key && \  
apt-key add FD-archive-key  
  
# Install OpenLDAP, ldap-utils and cfssl from baseimage  
# sources: https://github.com/osixia/docker-light-
baseimage/blob/stable/image/tool/add-service-available  
# https://github.com/osixia/docker-light-baseimage/blob/stable/image/service-
available/:cfssl/download.sh  
RUN apt-get -y update \  
&& /container/tool/add-service-available :cfssl \  
&& LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes
--no-install-recommends \  
ldap-utils \  
openssl \  
slapd \  
vim \  
wget \  
git \  
ssmtp \  
fusiondirectory \  
fusiondirectory-schema  
  
# Add service directory to /container/service  
ADD service /container/service  
  
# Use baseimage install-service script and clean all  
# https://github.com/osixia/docker-light-
baseimage/blob/stable/image/tool/install-service  
RUN /container/tool/install-service \  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
# Add default env variables  
ADD environment /container/environment/99-default  
  
# Set OpenLDAP data and config directories in a data volume  
VOLUME ["/var/lib/ldap", "/etc/ldap/slapd.d"]  
  
# Expose default ldap and ldaps ports  
EXPOSE 389 636  

