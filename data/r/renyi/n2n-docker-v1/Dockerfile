FROM centos:7  
MAINTAINER <renyinew@gmail.com>  
ENV VERSION v1  
  
RUN yum update -y && \  
yum groupinstall "Development Tools" -y && \  
yum install openssl-devel svn net-tools -y  
  
WORKDIR ['/root']  
  
RUN svn co https://shop.ntop.org/svn/ntop/trunk/n2n && \  
cd n2n/n2n_$VERSION && make && make install  
  
RUN yum groupremove "Development Tools" -y && \  
rm -rf /root/n2n /var/cache/yum/*  
  

