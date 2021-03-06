#  
# Copyright 2014-2015 by Cloudsoft Corporation Limited  
#  
# Licensed under the Apache License, Version 2.0 (the "License");  
# you may not use this file except in compliance with the License.  
# You may obtain a copy of the License at  
#  
# http://www.apache.org/licenses/LICENSE-2.0  
#  
# Unless required by applicable law or agreed to in writing, software  
# distributed under the License is distributed on an "AS IS" BASIS,  
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  
# See the License for the specific language governing permissions and  
# limitations under the License.  
FROM ubuntu  
#ARG ROOT_PASSWORD=p4ssw0rd  
MAINTAINER Cloudsoft "brooklyn@cloudsoftcorp.com"  
# CLOCKER_VERSION_BELOW  
LABEL version="1.1.0-SNAPSHOT"  
  
# setup locale  
RUN type locale-gen ; if [ "$?" -eq "0" ] ; then locale-gen en_US.UTF-8 ; fi  
  
# setup root account  
RUN echo 'root:p4ssw0rd' | chpasswd  
  
# install sshd  
RUN apt-get update ; \  
apt-get install -y openssh-server ; \  
mkdir /var/run/sshd ; \  
chmod 600 /var/run/sshd  
  
# create host keys if absent  
RUN if [ -f "/etc/ssh/ssh_host_dsa_key" -a -f "/etc/ssh/ssh_host_rsa_key" ] ;
then \  
echo "SSH host private keys already exists" ; \  
else \  
ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa ; \  
ssh-keygen -f /etc/ssh/ssh_host_dsa_key -N '' -t dsa ; \  
fi  
  
# configure sshd to allow login  
RUN sed -i.bk 's/PermitRootLogin.*$/PermitRootLogin yes/g'
/etc/ssh/sshd_config ; \  
echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config; \  
echo 'RSAAuthentication yes' >> /etc/ssh/sshd_config  
  
# SSH login fix. Otherwise user is kicked off after login  
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional
pam_loginuid.so@g' -i /etc/pam.d/sshd || true  
  
# Create the .ssh directory for mounting  
RUN mkdir /root/.ssh ; \  
chmod 700 /root/.ssh  
VOLUME [ "/root/.ssh" ]  
  
EXPOSE 22  
CMD [ "/usr/sbin/sshd", "-D" ]  

