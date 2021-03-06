FROM dstacademy/steamcmd:0.2.1  
MAINTAINER DST Academy <support@dst.academy>  
  
# Set build arguments.  
ARG DST_HOME  
ENV DST_HOME ${DST_HOME:-"/opt/dst"}  
ARG DST_BRANCH  
ENV DST_BRANCH ${DST_BRANCH}  
ARG DST_BRANCH_PASSWORD  
ENV DST_BRANCH_PASSWORD ${DST_BRANCH_PASSWORD}  
ARG DSTA_HOME  
ENV DSTA_HOME ${DSTA_HOME:-"/usr/local/share/dsta"}  
ARG CLUSTER_PATH  
ENV CLUSTER_PATH ${CLUSTER_PATH:-"/var/lib/dsta/cluster"}  
  
# Set environment variables.  
ENV DESCRIPTION="Powered by DST Academy." \  
SERVER_PORT="10999" \  
SHARD_NAME=shard \  
SHARD_BIND_IP="0.0.0.0" \  
BACKUP_LOG_COUNT=0  
# Add labels.  
LABEL academy.dst.config.update="true"  
  
# Install dependencies.  
RUN set -x \  
&& dpkg --add-architecture i386 \  
&& apt-get update \  
&& apt-get install -y --no-install-recommends \  
lib32stdc++6 \  
libcurl4-gnutls-dev:i386 \  
&& apt-get clean \  
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  
  
# Install Don't Starve Together Server.  
RUN set -x \  
&& mkdir -p $DST_HOME \  
&& chown $STEAM_USER:$STEAM_USER $DST_HOME \  
&& sync \  
&& gosu $STEAM_USER steamcmd \  
+@ShutdownOnFailedCommand 1 \  
+login anonymous \  
+force_install_dir $DST_HOME \  
+app_update 343050 \  
$([ -n "$DST_BRANCH" ] && printf %s "-beta $DST_BRANCH") \  
$([ -n "$DST_BRANCH_PASSWORD" ] && printf %s "-betapassword
$DST_BRANCH_PASSWORD") \  
validate \  
+quit \  
&& rm -rf $STEAM_HOME/Steam/logs $STEAM_HOME/Steam/appcache/httpcache \  
&& find $STEAM_HOME/package -type f ! -name "steam_cmd_linux.installed" !
-name "steam_cmd_linux.manifest" -delete  
  
# Copy common scripts.  
COPY /script/* /usr/local/bin/  
  
# Copy static files.  
COPY /static $DSTA_HOME  
  
# Create pipe for the game console.  
RUN set -x \  
&& mkfifo $DSTA_HOME/console \  
&& chown -R $STEAM_USER:$STEAM_USER $DSTA_HOME \  
&& mkdir -p $(dirname $CLUSTER_PATH) \  
&& chown $STEAM_USER:$STEAM_USER $(dirname $CLUSTER_PATH)  
  
# Copy entrypoint script.  
COPY /docker-entrypoint.sh /  
  
# Expose default server port.  
EXPOSE $SERVER_PORT/udp  
  
# Set up a volume for configuration files.  
VOLUME ["$CLUSTER_PATH"]  
  
# Set entrypoint and default command.  
ENTRYPOINT ["/docker-entrypoint.sh"]  
CMD ["dst-server", "start"]  

