FROM apendergast/ceg-docker-base:gateway-latest as gateway  
FROM apendergast/ceg-docker-base:ui-latest as ui  
COPY \--from=gateway /root/dummy /root/dummy  
WORKDIR /root/  
ARG GIT_BRANCH=master  
ARG TIMESTAMP=0  
# build gateway  
RUN echo "$TIMESTAMP" && git clone https://github.com/aloysius-pgast/crypto-
exchanges-gateway.git && cd crypto-exchanges-gateway && \  
git checkout $GIT_BRANCH && \  
cp -R /root/dummy/gateway/node_modules . && npm install --unsafe-perm && \  
cp docker/config.docker.json config/config.json  
# build ui  
RUN cd crypto-exchanges-gateway/ui && \  
cp -R /root/dummy/ui/node_modules . && npm install --unsafe-perm && npm run
build && rm -fr node_modules  
  
FROM apendergast/alpine-node:runtime-latest  
WORKDIR /root/crypto-exchanges-gateway/  
COPY \--from=ui /root/crypto-exchanges-gateway .  
  
ENV cfg.auth.apikey ""  
ENV cfg.listen.externalEndpoint ""  
ENV cfg.listenWs.externalEndpoint ""  
ENV cfg.exchanges.poloniex.key ""  
ENV cfg.exchanges.poloniex.secret ""  
ENV cfg.exchanges.bittrex.key ""  
ENV cfg.exchanges.bittrex.secret ""  
ENV cfg.exchanges.binance.key ""  
ENV cfg.exchanges.binance.secret ""  
EXPOSE 8000  
EXPOSE 8001  
CMD ["node", "./gateway.js"]  

