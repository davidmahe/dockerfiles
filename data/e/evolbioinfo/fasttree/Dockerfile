# FastTree  
# http://www.microbesonline.org/fasttree/#Install  
# v2.1.9  
# base image: Ubuntu  
FROM ubuntu:16.04  
# File Author / Maintainer  
MAINTAINER Frederic Lemoine <frederic.lemoine@pasteur.fr>  
  
RUN apt-get update --fix-missing \  
&& apt-get install -y wget gcc \  
&& cd /usr/local/ \  
&& wget http://www.microbesonline.org/fasttree/FastTree-2.1.9.c \  
&& gcc -DNO_SSE -O3 -finline-functions -funroll-loops -Wall -o bin/FastTree
FastTree-2.1.9.c -lm \  
&& rm FastTree-2.1.9.c \  
&& apt-get remove -y wget gcc \  
&& apt-get autoremove -y \  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/* \  
&& mkdir /pasteur  
  
ENTRYPOINT ["/usr/local/bin/FastTree"]  

