FROM python:3.6  
ENV S3_BUCKET_NAME 'S3_BUCKET_NAME '  
ENV AWS_ACCESS_KEY_ID 'AWS_ACCESS_KEY_ID'  
ENV AWS_SECRET_ACCESS_KEY 'AWS_SECRET_ACCESS_KEY'  
COPY config /root/.aws/  
  
RUN pip install awscli  

