FROM java:8-jdk  
  
ENV GRADLE_VERSION 2.6  
WORKDIR /usr/bin  
RUN curl -sLO
https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip &&
\  
unzip gradle-${GRADLE_VERSION}-all.zip && \  
ln -s gradle-${GRADLE_VERSION} gradle && \  
rm gradle-${GRADLE_VERSION}-all.zip  
  
ENV USER_SERVICE_URL http://54.233.122.209:8080/  
ENV GRADLE_HOME /usr/bin/gradle  
ENV PATH $PATH:$GRADLE_HOME/bin  
  
# Install app dependencies  
RUN cd /  
COPY . /application  
  
EXPOSE 4567  
WORKDIR /application  
RUN gradle jar  
  
CMD ["bash", "init.sh"]  

