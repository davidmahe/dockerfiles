FROM centos:centos6.6  
MAINTAINER yoku0825  
WORKDIR /root  
  
RUN yum upgrade -y  
RUN test -d /tmp/setup || mkdir /tmp/setup  
RUN ln -sf /usr/share/zoneinfo/Japan /etc/localtime  
  
RUN yum install -y http://dev.mysql.com/get/mysql57-community-release-
el6-7.noarch.rpm  
RUN yum install -y mysql-community-server mysql-utilities  
RUN yum install -y patch  
  
COPY . /tmp/setup  
RUN service mysqld start  
RUN patch /etc/my.cnf /tmp/setup/my.cnf.patch  
RUN patch /etc/mysql/fabric.cfg /tmp/setup/fabric.cfg.patch  
RUN bash /tmp/setup/init.sh  
  
CMD service mysqld start && mysqlfabric manage start  

