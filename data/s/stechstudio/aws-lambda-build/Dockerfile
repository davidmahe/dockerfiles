# Create amzn-ami-hvm-2016.03.3.x86_64-gp2 container suitable for building
Lambda binaries  
FROM awswift/amazonlinux:0.1  
LABEL authors="Bubba Hines <bubba@stechstudio.com>"  
  
COPY bash/.bashrc /root/.bashrc  
COPY bash/.bashrc_help /root/.bashrc_help  
  
# Build dependencies  
RUN yum makecache fast  
RUN rpm --rebuilddb && yum groupinstall -y "Development Tools"
\--setopt=group_package_types=mandatory,default  
RUN rpm --rebuilddb && yum install -y libmount-devel  
RUN rpm --rebuilddb && yum install -y jq cmake  
RUN rpm --rebuilddb && yum install -y texlive gtk-doc docbook-utils-pdf  
RUN rpm --rebuilddb && yum install -y gmp-devel libssh2-devel  
  
RUN mkdir -p /deps/advc  
RUN \  
curl -Ls
https://github.com/amadvance/advancecomp/releases/download/v2.0/advancecomp-2.0.tar.gz
| tar xzC /deps/advc --strip-components=1 \  
&& cd /deps/advc \  
&& ./configure && make && make install  
RUN rm -rf /deps  

