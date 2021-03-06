# VERSION latest  
# AUTHOR: Thomas Harning Jr <harningt@gmail.com>  
# DESCRIPTION: Alpine linux base image with s6-overlay injected  
FROM mhart/alpine-node:8  
MAINTAINER Andy Savage <andy@savage.hk>  
  
ARG S6_OVERLAY_RELEASE="v1.19.1.1"  
ARG TMP_BUILD_DIR="/tmp/build"  
# Pull in the overlay binaries  
ADD https://github.com/just-
containers/s6-overlay/releases/download/$S6_OVERLAY_RELEASE/s6-overlay-
nobin.tar.gz.sig "${TMP_BUILD_DIR}/"  
  
# Pull in the trust keys  
COPY keys/trust.gpg "${TMP_BUILD_DIR}/trust.gpg"  
  
RUN \  
addgroup -g 1000 node && \  
adduser -u 1000 -G node -s /bin/sh -D node  
  
# Patch in source for testing sources...  
# Update, install necessary packages, fixup permissions, delete junk  
RUN \  
apk add --update s6 s6-portable-utils ca-certificates wget tar bash curl g++
git make && \  
apk add --virtual verify gnupg && \  
mkdir -p "${TMP_BUILD_DIR}" && \  
chmod 700 "${TMP_BUILD_DIR}" && \  
cd "${TMP_BUILD_DIR}" && \  
wget -q -O "${TMP_BUILD_DIR}/s6-overlay-nobin.tar.gz" https://github.com/just-
containers/s6-overlay/releases/download/$S6_OVERLAY_RELEASE/s6-overlay-
nobin.tar.gz && \  
gpg --no-options --no-default-keyring --homedir "${TMP_BUILD_DIR}" \--keyring
./trust.gpg --no-auto-check-trustdb --trust-model always --verify "s6-overlay-
nobin.tar.gz.sig" "s6-overlay-nobin.tar.gz" && \  
apk del verify && \  
tar -C / -xzf "s6-overlay-nobin.tar.gz" && \  
cd / && \  
apk del wget tar && \  
rm -rf /var/cache/apk/* && \  
rm -rf ${TMP_BUILD_DIR}  
  
ENTRYPOINT [ "/init" ]  

