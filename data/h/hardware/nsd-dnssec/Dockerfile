FROM alpine:3.7  
LABEL description "Simple DNS authoritative server with DNSSEC support" \  
maintainer="Hardware <contact@meshup.net>"  
  
ARG NSD_VERSION=4.1.21  
# https://pgp.mit.edu/pks/lookup?search=0x7E045F8D&fingerprint=on&op=index  
# pub 4096R/7E045F8D 2011-04-21 W.C.A. Wijngaards <wouter@nlnetlabs.nl>  
ARG GPG_SHORTID="0x7E045F8D"  
ARG GPG_FINGERPRINT="EDFA A3F2 CA4E 6EB0 5681 AF8E 9F6F 1C2D 7E04 5F8D"  
ARG
SHA256_HASH="7858b934a07e1582079d7e724b05855380416b7fd68cdaeeca16305bd66bd2bd"  
ENV UID=991 GID=991  
RUN echo "@community https://nl.alpinelinux.org/alpine/v3.7/community" >>
/etc/apk/repositories \  
&& apk -U upgrade \  
&& apk add -t build-dependencies \  
gnupg \  
build-base \  
libevent-dev \  
openssl-dev \  
ca-certificates \  
&& apk add \  
ldns \  
ldns-tools \  
libevent \  
openssl \  
tini@community \  
&& cd /tmp \  
&& wget -q https://www.nlnetlabs.nl/downloads/nsd/nsd-${NSD_VERSION}.tar.gz \  
&& wget -q
https://www.nlnetlabs.nl/downloads/nsd/nsd-${NSD_VERSION}.tar.gz.asc \  
&& echo "Verifying both integrity and authenticity of
nsd-${NSD_VERSION}.tar.gz..." \  
&& CHECKSUM=$(sha256sum nsd-${NSD_VERSION}.tar.gz | awk '{print $1}') \  
&& if [ "${CHECKSUM}" != "${SHA256_HASH}" ]; then echo "ERROR: Checksum does
not match!" && exit 1; fi \  
&& ( \  
gpg --keyserver pgp.mit.edu --recv-keys ${GPG_SHORTID} || \  
gpg --keyserver keyserver.pgp.com --recv-keys ${GPG_SHORTID} || \  
gpg --keyserver ha.pool.sks-keyservers.net --recv-keys ${GPG_SHORTID} \  
) \  
&& FINGERPRINT="$(LANG=C gpg --verify nsd-${NSD_VERSION}.tar.gz.asc
nsd-${NSD_VERSION}.tar.gz 2>&1 \  
| sed -n "s#Primary key fingerprint: \\(.*\\)#\1#p")" \  
&& if [ -z "${FINGERPRINT}" ]; then echo "ERROR: Invalid GPG signature!" &&
exit 1; fi \  
&& if [ "${FINGERPRINT}" != "${GPG_FINGERPRINT}" ]; then echo "ERROR: Wrong
GPG fingerprint!" && exit 1; fi \  
&& echo "All seems good, now unpacking nsd-${NSD_VERSION}.tar.gz..." \  
&& tar xzf nsd-${NSD_VERSION}.tar.gz && cd nsd-${NSD_VERSION} \  
&& ./configure \  
CFLAGS="-O2 -flto -fPIE -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=2 -fstack-
protector-strong -Wformat -Werror=format-security" \  
LDFLAGS="-Wl,-z,now -Wl,-z,relro" \  
&& make && make install \  
&& apk del build-dependencies \  
&& rm -rf /var/cache/apk/* /tmp/* /root/.gnupg  
  
COPY bin /usr/local/bin  
VOLUME /zones /etc/nsd /var/db/nsd  
EXPOSE 53 53/udp  
CMD ["run.sh"]  

