#  
# NOTE: This Dockerfile is generated.  
#  
# Do not edit this file directly.  
FROM openjdk:8-jdk  
  
# Install scala  
RUN mkdir -p /usr/share/scala-2.12.4; \  
curl -fsL https://downloads.typesafe.com/scala/2.12.4/scala-2.12.4.tgz | tar
xfz - -C /usr/share/scala-2.12.4 && \  
echo export PATH="/usr/share/scala-2.12.4/bin:$PATH" >> $HOME/.bashrc  
  
# sbt requires bc to be installed  
RUN apt-get update && apt-get install bc  
  
# Install sbt  
RUN mkdir -p /usr/share/ && \  
curl -L https://github.com/sbt/sbt/releases/download/v1.0.3/sbt-1.0.3.tgz |
tar xfz - -C /usr/share/ && \  
echo export PATH="/usr/share//sbt/bin:$PATH" >> $HOME/.bashrc && \  
/usr/share//sbt/bin/sbt sbtVersion  

