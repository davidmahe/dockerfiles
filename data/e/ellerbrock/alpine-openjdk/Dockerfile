# Developer: Maik Ellerbrock <opensource@frapsoft.com>  
#  
# GitHub: https://github.com/ellerbrock  
# Twitter: https://twitter.com/frapsoft  
# Docker: https://hub.docker.com/u/ellerbrock  
# Quay: https://quay.io/user/ellerbrock  
FROM alpine:3.7  
LABEL com.frapsoft.maintainer="Maik Ellerbrock" \  
com.frapsoft.version="0.1.2"  
  
# Optional Configuration Parameter  
ARG SERVICE_USER  
ARG SERVICE_HOME  
  
# Default Settings  
ENV SERVICE_USER ${SERVICE_USER:-java}  
ENV SERVICE_HOME ${SERVICE_HOME:-/home/${SERVICE_USER}}  
  
RUN \  
adduser -h ${SERVICE_HOME} -s /sbin/nologin -u 1000 -D ${SERVICE_USER} && \  
apk add --no-cache \  
openjdk8 \  
dumb-init  
  
USER ${SERVICE_USER}  
WORKDIR ${SERVICE_HOME}  
VOLUME ${SERVICE_HOME}  
  
ENTRYPOINT [ "/usr/bin/dumb-init" ]  
CMD [ "java" ]  

