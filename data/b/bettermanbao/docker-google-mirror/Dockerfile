FROM alpine:3.5  
ENV NGINX_VER 1.10.3  
RUN apk add --update git openssl-dev pcre-dev zlib-dev wget build-base && \  
mkdir src && cd src && \  
wget http://nginx.org/download/nginx-${NGINX_VER}.tar.gz && \  
tar xzf nginx-${NGINX_VER}.tar.gz && \  
git clone https://github.com/cuber/ngx_http_google_filter_module && \  
git clone https://github.com/yaoweibin/ngx_http_substitutions_filter_module &&
\  
cd nginx-${NGINX_VER} && \  
./configure --prefix=/opt/nginx \  
\--with-http_ssl_module \  
\--add-module=../ngx_http_google_filter_module \  
\--add-module=../ngx_http_substitutions_filter_module && \  
make && make install && \  
apk del git build-base && \  
rm -rf /src && \  
rm -rf /var/cache/apk/*  
  
ADD nginx.conf /opt/nginx/conf/nginx.conf  
  
EXPOSE 80  
CMD ["/opt/nginx/sbin/nginx", "-g", "daemon off;"]  

