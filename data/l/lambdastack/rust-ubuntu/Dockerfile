FROM ubuntu:latest  
MAINTAINER Chris Jones "chris.jones@lambdastack.io"  
ENV DEBIAN_FRONTEND=noninteractive  
  
RUN apt-get update && \  
apt-get install \  
git \  
ca-certificates \  
curl \  
gcc \  
libc6-dev \  
openssl \  
libssl-dev \  
pkg-config \  
-qqy \  
\--no-install-recommends \  
&& rm -rf /var/lib/apt/lists/*  
  
ENV RUST_ARCHIVE=rust-1.14.0-x86_64-unknown-linux-gnu.tar.gz  
ENV RUST_DOWNLOAD_URL=https://static.rust-lang.org/dist/$RUST_ARCHIVE  
  
RUN mkdir /rust  
WORKDIR /rust  
  
RUN curl -fsOSL $RUST_DOWNLOAD_URL \  
&& curl -s $RUST_DOWNLOAD_URL.sha256 | sha256sum -c - \  
&& tar -C /rust -xzf $RUST_ARCHIVE \--strip-components=1 \  
&& rm $RUST_ARCHIVE \  
&& ./install.sh  

