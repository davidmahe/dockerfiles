FROM dockerfile/nodejs-bower-grunt  
RUN apt-get install -y build-essential  
RUN mkdir /opt/copay  
WORKDIR /opt/copay  
RUN \  
curl -s -L https://github.com/justcoin/copay/tarball/master | tar zx -C
/opt/copay/ --strip-components=1 && \  
npm install && \  
bower install --production --force --allow-root --config.interactive=false &&
\  
grunt  
EXPOSE 80  
CMD PORT=80 npm start  
  

