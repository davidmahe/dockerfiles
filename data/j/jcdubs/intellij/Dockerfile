FROM ubuntu:14.04  
MAINTAINER Jason Conway-Williams "jasonconwaywilliams@gmail.com"  
  
RUN sed 's/main$/main universe/' -i /etc/apt/sources.list && \  
apt-get update && apt-get install -y software-properties-common && \  
add-apt-repository ppa:webupd8team/java -y && \  
apt-get update && \  
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true |
/usr/bin/debconf-set-selections && \  
apt-get install -y oracle-java8-installer libxext-dev libxrender-dev libxtst-
dev && \  
apt-get install -y fonts-dejavu-core && \  
apt-get install -y libcurl3 php5-curl curl unzip zip && \  
apt-get install -y git && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/* && \  
rm -rf /tmp/*  
  
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle  
ENV IDEA_JDK /usr/lib/jvm/java-8-oracle  
ENV IDEA_JDK_64 /usr/lib/jvm/java-8-oracle  
ENV SDKMAN_DIR /home/developer/sdkman  
  
RUN mkdir -p /home/developer && \  
echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >>
/etc/passwd && \  
echo "developer:x:1000:" >> /etc/group && \  
echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \  
chmod 0440 /etc/sudoers.d/developer && \  
chown developer:developer -R /home/developer  
  
RUN wget -P /tmp/ https://download.jetbrains.com/idea/ideaIC-2016.3.4.tar.gz
&& \  
tar -xf /tmp/ideaIC-2016.3.4.tar.gz -C /opt && \  
rm -rf /tmp/*  
  
COPY intellij-entry-point.sh /  
  
RUN chmod +x /intellij-entry-point.sh  
  
USER developer  
  
ENV HOME /home/developer  
WORKDIR /home/developer  
  
ENTRYPOINT ["/intellij-entry-point.sh"]  

