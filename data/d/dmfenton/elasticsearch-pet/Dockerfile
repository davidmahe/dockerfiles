FROM elasticsearch:5.1.1  
RUN bin/elasticsearch-plugin install io.fabric8:elasticsearch-cloud-
kubernetes:5.1.1  
  
ENV BOOTSTRAP_MLOCKALL=false NODE_DATA=true NODE_MASTER=true
JAVA_OPTS=-Djava.net.preferIPv4Stack=true  
  
# pre-stop-hook.sh and dependencies  
RUN apt-get update && apt-get install -y \  
jq \  
curl \  
&& rm -rf /var/lib/apt/lists/*  
COPY pre-stop-hook.sh /pre-stop-hook.sh  
  
RUN echo vm.max_map_count=262144 >> /etc/sysctl.conf  
  
COPY elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml  

