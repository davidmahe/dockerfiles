FROM openjdk:8  
ENV DEBIAN_FRONTEND noninteractive  
RUN apt-get -qqy update && apt-get install -y --no-install-recommends\  
chromium\  
bzip2 \  
apt-utils \  
gconf2 \  
unzip \  
curl \  
libfontconfig \  
gcc \  
g++ \  
python-dev \  
apt-transport-https \  
python-setuptools \  
lsb-release \  
openssh-client \  
git;  
  
RUN easy_install -U pip && \  
pip install -U crcmod  
  
ENV CLOUD_SDK_VERSION 200.0.0  
RUN echo "deb https://packages.cloud.google.com/apt cloud-sdk-$(lsb_release
-cs) main" > /etc/apt/sources.list.d/google-cloud-sdk.list \  
&& curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key
add - \  
&& apt-get update -qqy && apt-get install -qqy \  
google-cloud-sdk=${CLOUD_SDK_VERSION}-0 \  
google-cloud-sdk-app-engine-java \  
&& rm -rf /var/lib/apt/lists/* /var/cache/apt/*  
  
RUN echo "deb [arch=amd64] https://download.docker.com/linux/debian
$(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list \  
&& curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \  
&& apt-get update -qqy && apt-get install -qqy docker-ce \  
&& rm -rf /var/lib/apt/lists/* /var/cache/apt/*  
  
ENV CHROME_DRIVER_VERSION 2.38  
RUN curl -Ls
https://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip
> ~/chromedriver.zip \  
&& unzip ~/chromedriver.zip -d /usr/bin \  
&& rm ~/chromedriver.zip  
  
RUN gcloud config set core/disable_usage_reporting true && \  
gcloud config set component_manager/disable_update_check true && \  
gcloud config set metrics/environment github_docker_image  
  
# Setup teamcity-agent and his data dir  
RUN adduser --disabled-password --gecos "" teamcity-agent --ingroup docker &&\  
mkdir -p /data &&\  
chown -R teamcity-agent:root /data  
  
# Install node version manager  
USER teamcity-agent  
ENV NVM_VERSION v0.33.11  
#For karma  
ENV CHROME_BIN=/usr/bin/chromium  
RUN curl -so-
https://raw.githubusercontent.com/creationix/nvm/$NVM_VERSION/install.sh | sh  
  
USER root  
EXPOSE 9090  
COPY docker-entrypoint.sh /  
CMD /docker-entrypoint.sh  

