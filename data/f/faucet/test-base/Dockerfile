## Image name: faucet/test-base  
## Base image for FAUCET tests.  
FROM ubuntu:16.04  
ENV OVSV="v2.9.0"  
ENV DPDK="18.02.1"  
ENV MININETV="2.2.2"  
ENV OVSDEPS="autoconf automake libpcap-dev libcap-ng-dev libnuma-dev libtool
libssl-dev linux-headers-generic libffi-dev"  
ENV AG="apt-get -qqy --no-install-recommends -o=Dpkg::Use-Pty=0"  
ENV DEBIAN_FRONTEND=noninteractive  
# Pre-install Ryu and basic dependencies - so test image has less work  
ENV PIPDEPS="setuptools wheel virtualenv"  
ENV PIP="pip -q --no-cache-dir install --upgrade"  
ENV PIP3="pip3 -q --no-cache-dir install --upgrade"  
ENV SETUPQ="setup.py -q"  
ENV MAKEFLAGS="-s"  
ENV BUILDDIR="/var/tmp/build"  
ENV DPDK_TARGET=x86_64-native-linuxapp-gcc  
  
###  
### When apt-get'ing, make sure apt-update always run first per RUN  
### to ensure Docker layer cache doesn't use a stale apt database.  
###  
COPY setupproxy.sh /  
  
RUN \  
./setupproxy.sh && \  
$AG update && \  
$AG install \  
$OVSDEPS \  
apt-transport-https \  
bc \  
bridge-utils \  
build-essential \  
curl \  
dsniff \  
fping \  
gcc \  
git \  
iperf \  
iputils-ping \  
iproute2 \  
ladvd \  
libnuma-dev \  
libpython2.7-dev \  
libpython3-dev \  
libyaml-dev \  
lsof \  
netcat \  
ndisc6 \  
net-tools \  
netcat-openbsd \  
nmap \  
numactl \  
openvswitch-common \  
parallel \  
patch \  
psmisc \  
python-pip \  
python3-pip \  
python-six \  
software-properties-common \  
sudo \  
tcpdump \  
tshark \  
vlan \  
wget \  
wpasupplicant && \  
$AG install linux-headers-`uname -r` && \  
git config --global url.https://github.com/.insteadOf git://github.com/ && \  
mkdir -p $BUILDDIR && \  
cd $BUILDDIR && \  
wget -q -O- http://fast.dpdk.org/rel/dpdk-$DPDK.tar.xz | tar -Jxf- && \  
cd dpdk* && \  
make install T=$DPDK_TARGET DESTDIR=install && \  
cd .. && \  
git clone https://github.com/openvswitch/ovs -b ${OVSV} && \  
cd ovs && \  
./boot.sh && \  
./configure --enable-silent-rules --quiet --with-dpdk=`echo
../dpdk*/$DPDK_TARGET` && \  
make install && \  
cd .. && \  
git clone https://github.com/mininet/mininet -b $MININETV && \  
cd mininet && \  
perl -pi -e "s/setup.py/${SETUPQ}/g" Makefile && \  
perl -pi -e "s/apt-get/${AG}/g" util/install.sh && \  
for i in ssh pep8 pyflakes python-pexpect pylint xterm ; do \  
perl -pi -e "s/${i}//g" util/install.sh ; done && \  
util/install.sh -n && \  
cd .. && \  
git clone https://github.com/google/pytype.git && \  
cd pytype && \  
git submodule init && \  
git submodule update && \  
python2 $SETUPQ install && \  
cd .. && \  
cd / && rm -rf $BUILDDIR && \  
$AG purge $OVSDEPS linux-headers-`uname -r` && \  
$AG autoremove  
  
RUN \  
./setupproxy.sh && \  
$AG update && \  
$AG install cython3 && \  
$AG purge pylint && \  
$PIP multiprocessing scapy==2.3.2 $PIPDEPS && \  
$PIP3 $PIPDEPS && \  
$PIP ryu && \  
$PIP3 ryu  
  
# Install docker in docker...  
RUN ./setupproxy.sh && \  
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
&& \  
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu
$(lsb_release -cs) stable" && \  
$AG update && $AG install docker-ce  

