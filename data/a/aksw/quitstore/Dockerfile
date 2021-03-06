FROM python:3  
MAINTAINER Norman Radtke <radtke@informatik.uni-leipzig.de>  
MAINTAINER Natanael Arndt <arndt@informatik.uni-leipzig.de>  
ENV SSH_AUTH_SOCK /var/run/ssh-agent.sock  
  
RUN apt-get update && apt-get -y install \  
git \  
cmake \  
libffi-dev \  
libssl-dev \  
libssh2-1-dev \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN git clone \--depth 1 --branch v0.25.1
https://github.com/libgit2/libgit2.git \  
&& cd libgit2 \  
&& mkdir build && cd build \  
&& cmake .. \  
&& cmake --build . --target install \  
&& ldconfig \  
&& cd ../.. && rm -r libgit2  
  
RUN mkdir -p /usr/src/app  
WORKDIR /usr/src/app  
  
COPY quit/ /usr/src/app/quit  
COPY requirements.txt /usr/src/app/  
RUN pip install --no-cache-dir -r requirements.txt \  
&& ln -s /usr/src/app/quit/run.py /usr/local/bin/quit  
  
COPY docker/config.ttl /etc/quit/  
  
ENV QUIT_CONFIGFILE="/etc/quit/config.ttl"  
ENV QUIT_LOGFILE="/var/log/quit.log"  
RUN mkdir /data  
  
VOLUME /data  
VOLUME /etc/quit  
EXPOSE 80  
# Set default git user  
RUN git config --global user.name QuitStore && git config --global user.email
quitstore@example.org  
  
CMD uwsgi --socket 0.0.0.0:80 --protocol=http -w quit.run --pyargv "-vv"  

