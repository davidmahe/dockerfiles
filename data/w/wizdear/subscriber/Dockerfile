FROM gliderlabs/alpine:3.4  
RUN apk add --update ca-certificates && \  
rm -rf /var/cache/apk/* /tmp/*  
RUN apk add --no-cache tzdata  
ENV TZ Asia/Seoul  
RUN update-ca-certificates  
RUN mkdir /app  
ADD . /app/  
WORKDIR /app  
CMD []  
ENTRYPOINT ["/app/main"]  
  

