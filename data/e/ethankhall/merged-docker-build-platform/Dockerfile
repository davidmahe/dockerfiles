FROM openjdk:8-jdk-alpine  
  
RUN echo "http://dl-4.alpinelinux.org/alpine/edge/community" >>
/etc/apk/repositories && \  
apk add --no-cache docker curl python bash coreutils tar unzip gzip openssh-
client git  
  
ENV HOME /  
  
ARG CLOUD_SDK_VERSION=153.0.0  
ARG SHA256SUM=ade29e765f7847bf6081affb6eada69b45138d4abb443b1484e891312990e958  
  
RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-
cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz  
RUN echo "${SHA256SUM} google-cloud-
sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz" > google-cloud-
sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz.sha256  
RUN sha256sum -c google-cloud-
sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz.sha256  
RUN tar xzf google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz  
  
ENV PATH /google-cloud-sdk/bin:$PATH  
RUN gcloud config set core/disable_usage_reporting true  
RUN gcloud config set component_manager/disable_update_check true  
RUN rm google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz.sha256
google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz  
RUN mkdir -p $HOME/.ssh && chmod 0700 $HOME/.ssh  
VOLUME ["/.config"]  

