FROM rocker/rstudio  
  
USER root  
  
# Spark dependencies  
ENV APACHE_SPARK_VERSION 2.1.0  
ENV HADOOP_VERSION 2.7  
# Temporarily add jessie backports to get openjdk 8, but then remove that
source  
RUN echo 'deb http://cdn-fastly.deb.debian.org/debian jessie-backports main' >
/etc/apt/sources.list.d/jessie-backports.list && \  
apt-get -y update && apt-get install -y libcups2 && apt-get install -y
libcups2-dev && \  
apt-get install --no-install-recommends -t jessie-backports -y openjdk-8-jre-
headless ca-certificates-java && \  
rm /etc/apt/sources.list.d/jessie-backports.list && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
RUN cd /tmp && \  
wget -q
http://d3kbcqa49mib13.cloudfront.net/spark-${APACHE_SPARK_VERSION}-bin-
hadoop${HADOOP_VERSION}.tgz && \  
echo
"3fc94096ae34f9a1a148d37e5ed640a7e5de1812f1f2ecd715d92bbf2901e895cf4b93e6d8ee0d64debb5df7c56d673c0a36e5fc49503ec0f4507eb0edf961a4
*spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" | sha512sum -c
- && \  
tar xzf spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -C
/usr/local && \  
rm spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz  
RUN cd /usr/local && ln -s spark-${APACHE_SPARK_VERSION}-bin-
hadoop${HADOOP_VERSION} spark  
  
# Mesos dependencies  
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv E56151BF && \  
DISTRO=debian && \  
CODENAME=jessie && \  
echo "deb http://repos.mesosphere.io/${DISTRO} ${CODENAME} main" >
/etc/apt/sources.list.d/mesosphere.list && \  
apt-get -y update && apt-get install -y systemd && \  
apt-get --no-install-recommends -y --force-yes install
mesos=1.1.0-2.0.107.debian81 && \  
apt-get clean && \  
rm -rf /var/lib/apt/lists/*  
  
# Spark and Mesos config  
ENV SPARK_HOME /usr/local/spark  
ENV MESOS_NATIVE_LIBRARY /usr/local/lib/libmesos.so  
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M
--driver-java-options=-Dlog4j.logLevel=info  
  
RUN R -e "install.packages('sparklyr', repos='http://cran.rstudio.com/',
dependencies=T)"  
  
USER $NB_USER

