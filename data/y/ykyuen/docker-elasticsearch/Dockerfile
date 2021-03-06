FROM openjdk:8-jre  
MAINTAINER pjpires@gmail.com  
  
# Export HTTP & Transport  
EXPOSE 9200 9300  
ENV VERSION 2.4.1  
# Install Elasticsearch.  
RUN apt update && apt install -y sudo uuid-runtime && \  
( curl -Lskj
https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$VERSION/elasticsearch-$VERSION.tar.gz
| \  
gunzip -c - | tar xf - ) && \  
mv /elasticsearch-$VERSION /elasticsearch && \  
rm -rf $(find /elasticsearch | egrep
"(\\.(exe|bat)$|sigar/.*(dll|winnt|x86-linux|solaris|ia64|freebsd|macosx))")  
  
# Volume for Elasticsearch data  
VOLUME ["/data"]  
  
# Copy configuration  
COPY config /elasticsearch/config  
  
# Copy run script  
COPY run.sh /  
  
# Set environment variables defaults  
ENV ES_HEAP_SIZE 512m  
ENV CLUSTER_NAME elasticsearch-default  
ENV NODE_MASTER true  
ENV NODE_DATA true  
ENV HTTP_ENABLE true  
ENV NETWORK_HOST _site_  
ENV HTTP_CORS_ENABLE true  
ENV HTTP_CORS_ALLOW_ORIGIN *  
ENV NUMBER_OF_MASTERS 1  
ENV NUMBER_OF_SHARDS 1  
ENV NUMBER_OF_REPLICAS 0  
CMD ["/run.sh"]  

