###########################################################  
#  
# Dockerfile for Dockerhub-webhook-api  
#  
###########################################################  
  
# Setting the base to nodejs 6  
FROM mhart/alpine-node:6  
  
# Maintainer  
MAINTAINER Jonas Enge  
  
#### Begin setup ####  
  
# Installs docker  
RUN apk add --update --no-cache docker py-pip  
RUN pip install docker-compose  
  
# Extra tools for native dependencies  
#RUN apk add --no-cache make gcc g++ python  
  
# Bundle app source  
COPY . /src  
  
# Change working directory  
WORKDIR "/src"  
  
# Install dependencies  
RUN npm install --production  
  
# Env variables  
ENV SERVER_PORT 3000  
ENV API_ROUTE /api  
ENV TOKEN abc123  
  
# Expose 3000  
EXPOSE 3000  
  
# Startup  
ENTRYPOINT node index.js  

