FROM debian:stable-20180213  
  
RUN apt-get update \  
&& DEBIAN_FRONTEND=noninteractive apt-get \--no-install-recommends --yes
install \  
offlineimap \  
ca-certificates \  
curl  
  
ENV
SUPERCRONIC_URL=https://github.com/aptible/supercronic/releases/download/v0.1.5/supercronic-
linux-amd64 \  
SUPERCRONIC=supercronic-linux-amd64 \  
SUPERCRONIC_SHA1SUM=9aeb41e00cc7b71d30d33c57a2333f2c2581a201  
  
RUN curl -fsSLO "$SUPERCRONIC_URL" \  
&& echo "${SUPERCRONIC_SHA1SUM} ${SUPERCRONIC}" | sha1sum -c - \  
&& chmod +x "$SUPERCRONIC" \  
&& mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" \  
&& ln -s "/usr/local/bin/${SUPERCRONIC}" /usr/local/bin/supercronic  
  
RUN useradd --home-dir /email --no-create-home offlineimap  
  
ADD crontab /etc/crontab  
  
ADD entrypoint /entrypoint  
  
RUN chmod 755 /entrypoint  
  
USER offlineimap  
  
ENTRYPOINT ["/entrypoint"]  

