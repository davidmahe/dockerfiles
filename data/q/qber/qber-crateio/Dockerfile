## -*- docker-image-name: "docker-crate" -*-  
#  
# Crate Dockerfile  
# https://github.com/crate/docker-crate  
#  
FROM java:8-jre  
MAINTAINER Crate Technology GmbH <office@crate.io>  
  
RUN apt-get update && \  
apt-get install -y python3 && \  
rm -rf /var/lib/apt && \  
ln -s /usr/bin/python3 /usr/bin/python  
  
ENV CRATE_VERSION 0.52.4  
RUN mkdir /crate && \  
wget -nv -O -
"https://cdn.crate.io/downloads/releases/crate-$CRATE_VERSION.tar.gz" \  
| tar -xzC /crate --strip-components=1  
  
ENV PATH /crate/bin:$PATH  
  
VOLUME ["/data"]  
  
ADD config/crate.yml /crate/config/crate.yml  
ADD config/logging.yml /crate/config/logging.yml  
  
WORKDIR /data  
  
# http: 4200 tcp  
# transport: 4300 tcp  
EXPOSE 4200 4300  
CMD ["crate", "-Des.config=/crate/config/crate.yml"]  
  
## END  

