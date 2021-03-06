FROM frolvlad/alpine-glibc:alpine-3.7  
MAINTAINER https://github.com/GhoulLord/docker_factorio_server  
  
ARG USER=factorio  
ARG GROUP=factorio  
ARG PUID=1004  
ARG PGID=1002  
ENV PORT=34197 \  
RCON_PORT=27015 \  
VERSION=0.16.41 \  
SHA1=52e833f39769bab7ea2eef823d8f1d64508610b1 \  
SAVES=/factorio/saves \  
CONFIG=/factorio/config \  
MODS=/factorio/mods \  
SCENARIOS=/factorio/scenarios  
  
RUN mkdir -p /opt /factorio && \  
apk add --update --no-cache pwgen && \  
apk add --update --no-cache --virtual .build-deps curl && \  
curl -sSL https://www.factorio.com/get-download/$VERSION/headless/linux64 \  
-o /tmp/factorio_headless_x64_$VERSION.tar.xz && \  
echo "$SHA1 /tmp/factorio_headless_x64_$VERSION.tar.xz" | sha1sum -c && \  
tar xf /tmp/factorio_headless_x64_$VERSION.tar.xz --directory /opt && \  
chmod ugo=rwx /opt/factorio && \  
rm /tmp/factorio_headless_x64_$VERSION.tar.xz && \  
ln -s $SAVES /opt/factorio/saves && \  
ln -s $MODS /opt/factorio/mods && \  
ln -s $SCENARIOS /opt/factorio/scenarios && \  
apk del .build-deps && \  
addgroup -g $PGID -S $GROUP && \  
adduser -u $PUID -G $GROUP -s /bin/sh -SDH $USER && \  
chown -R $USER:$GROUP /opt/factorio /factorio  
  
VOLUME /factorio  
  
EXPOSE $PORT/udp $RCON_PORT/tcp  
  
COPY files/ /  
  
RUN ["chmod", "+x", "/docker-entrypoint.sh"]  
  
USER $USER  
ENTRYPOINT ["/docker-entrypoint.sh"]  

