FROM nextcloud:fpm  
  
RUN apt-get update && apt-get install --no-install-recommends -y \  
supervisor \  
cron \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN mkdir /var/log/supervisord /var/run/supervisord && \  
echo "*/5 * * * * su - www-data -s /bin/bash -c \"php -f
/var/www/html/cron.php\""| crontab -  
  
COPY supervisord.conf /etc/supervisor/supervisord.conf  
  
CMD ["/usr/bin/supervisord"]  

