FROM ubuntu:14.04  
MAINTAINER @x110dc  
  
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-
selections  
RUN apt-get update -qq && \  
apt-get install -yq language-pack-en-base && \  
apt-get install -yq python python-pip && \  
dpkg-reconfigure locales  
RUN pip install stripe==1.31.0 salesforce-bulk==1.1.0 simple-
salesforce==0.68.1 celery==3.1.23  
  
COPY *.py /app/  
CMD ["python", "/app/reconcile-email.py"]  

