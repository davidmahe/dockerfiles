FROM gliderlabs/alpine  
  
MAINTAINER John Hill <unlikelyzero@gmail.com>  
  
# Installs bash and python  
RUN apk --update add bash python py-pip  
  
RUN pip install requests==2.5.1  
  
WORKDIR /root  
  
ADD scripts/go.py /root/go.py  
  
RUN chmod a+x /root/go.py  
  
CMD ["/root/go.py"]  

