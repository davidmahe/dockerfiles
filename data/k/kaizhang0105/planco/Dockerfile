FROM node:slim  
MAINTAINER kaizhang0105@163.com  
WORKDIR /tmp  
RUN npm install -g protractor mocha cucumber && \  
webdriver-manager update && \  
apt-get update && \  
apt-get install -y xvfb wget openjdk-7-jre && \  
wget -c https://dl.google.com/linux/direct/google-chrome-
stable_current_amd64.deb && \  
dpkg --unpack google-chrome-stable_current_amd64.deb && \  
apt-get install -f -y && \  
apt-get clean && \  
rm google-chrome-stable_current_amd64.deb && \  
mkdir /protractor  
ADD protractor.sh /protractor.sh  
# Fix for the issue with Selenium, as described here:  
# https://github.com/SeleniumHQ/docker-selenium/issues/87  
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null  
WORKDIR /protractor  
ENTRYPOINT /bin/bash  

