FROM openjdk:8-jdk-alpine  
  
# Install required packages  
RUN apk add \--no-cache \  
bash \  
python \  
su-exec \  
vim \  
wget \  
curl \  
git \  
maven \  
unzip \  
bash  
  
  
ENV STORM_USER=storm \  
STORM_CONF_DIR=/conf \  
STORM_DATA_DIR=/data \  
STORM_LOG_DIR=/logs  
  
# Add a user and make dirs  
RUN set -x \  
&& adduser -D "$STORM_USER" \  
&& mkdir -p "$STORM_CONF_DIR" "$STORM_DATA_DIR" "$STORM_LOG_DIR" \  
&& chown -R "$STORM_USER:$STORM_USER" "$STORM_CONF_DIR" "$STORM_DATA_DIR"
"$STORM_LOG_DIR"  
  
ARG GPG_KEY=ACEFE18DD2322E1E84587A148DE03962E80B8FFD  
ARG DISTRO_NAME=apache-storm-1.1.0  
  
# Download Apache Storm, verify its PGP signature, untar and clean up  
RUN set -x \  
&& apk add \--no-cache --virtual .build-deps \  
gnupg \  
&& wget -q "http://www.apache.org/dist/storm/$DISTRO_NAME/$DISTRO_NAME.tar.gz"
\  
&& wget -q
"http://www.apache.org/dist/storm/$DISTRO_NAME/$DISTRO_NAME.tar.gz.asc" \  
&& export GNUPGHOME="$(mktemp -d)" \  
&& gpg --keyserver ha.pool.sks-keyservers.net --recv-key "$GPG_KEY" \  
&& gpg --batch --verify "$DISTRO_NAME.tar.gz.asc" "$DISTRO_NAME.tar.gz" \  
&& tar -xzf "$DISTRO_NAME.tar.gz" \  
&& chown -R "$STORM_USER:$STORM_USER" "$DISTRO_NAME" #\  
#&& rm -r "$GNUPGHOME" "$DISTRO_NAME.tar.gz" "$DISTRO_NAME.tar.gz.asc" #\  
#&& apk del .build-deps  
  
WORKDIR $DISTRO_NAME  
RUN set -x \  
&& wget -q "https://github.com/DigitalPebble/storm-crawler/archive/master.zip"
\  
&& unzip master.zip \  
&& chown -R "$STORM_USER:$STORM_USER" storm-crawler-master  
  
  
ENV PATH $PATH:/$DISTRO_NAME/bin  
  
COPY docker-entrypoint.sh /  
#ENTRYPOINT ["/docker-entrypoint.sh"]

