FROM debian:jessie  
MAINTAINER Renzo Meister <rm@jamotion.ch>  
  
ENV DEBIAN_FRONTEND noninteractive  
  
## Install build deps, build and cleanup in one shot  
RUN apt-get update \  
&& apt-get -y --no-install-recommends install \  
automake \  
build-essential \  
ca-certificates \  
git \  
libc-ares2 \  
libc-ares-dev \  
libev4 \  
libev-dev \  
libevent-2.0-5 \  
libevent-dev \  
libssl1.0.0 \  
libssl-dev \  
libtool \  
pkg-config \  
wget \  
&& mkdir -p /opt && cd /opt \  
&& git clone https://github.com/pgbouncer/pgbouncer.git \  
&& cd /opt/pgbouncer \  
&& git checkout pgbouncer_1_7_2 \  
&& git submodule init \  
&& git submodule update \  
&& ./autogen.sh \  
&& ./configure --enable-evdns=no \  
&& make \  
&& make install \  
&& apt-get remove -y \  
automake \  
build-essential \  
ca-certificates \  
git \  
libc-ares-dev \  
libev-dev \  
libevent-dev \  
libssl-dev \  
libtool \  
pkg-config \  
wget \  
&& apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*  
  
## After `make install` pgbouncer needs some extra touches to make it work  
RUN mkdir -p /etc/pgbouncer/  
RUN mkdir -p /var/run/postgresql/  
RUN groupadd --system postgres  
RUN useradd -g postgres postgres  
RUN mkdir -p /var/log/postgresql  
RUN chown postgres:postgres /var/log/postgresql/  
RUN chown postgres:postgres /var/run/postgresql/  
  
ENV PG_ENV_POSTGRESQL_MAX_CLIENT_CONN 10000  
ENV PG_ENV_POSTGRESQL_DEFAULT_POOL_SIZE 50  
ENV PG_ENV_POSTGRESQL_SERVER_IDLE_TIMEOUT 240  
ADD run.sh /usr/local/bin/run  
RUN chmod +x /usr/local/bin/run  
  
EXPOSE 6432  
CMD ["/usr/local/bin/run"]  

