FROM node:8.9.1-alpine  
  
RUN mkdir -p /usr/src/app/server  
  
WORKDIR /usr/src/app  
ADD ./client ./client  
ADD ./server ./server  
  
RUN cd client && \  
npm install && \  
npm run build && \  
cd .. &&\  
\  
cd server && \  
npm install && \  
npm run build && \  
npm prune --production && \  
\  
rm -r ../client  
  
WORKDIR /usr/src/app/server  
  
CMD [ "npm", "start" ]  
  
EXPOSE 3000  

