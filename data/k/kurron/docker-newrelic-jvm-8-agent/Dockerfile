# Pre-built JDK 8 image  
FROM kurron/docker-oracle-jdk-8:latest  
  
MAINTAINER Ron Kurr <kurr@jvmguy.com>  
  
ADD newrelic /opt/example/newrelic  
  
ENV NEW_RELIC_APP_NAME ${NEW_RELIC_APP_NAME:-Not Set}  
#ENV NEW_RELIC_HOST_DISPLAY_NAME ${NEW_RELIC_HOST_DISPLAY_NAME:-Not Set}  
ENV NEW_RELIC_LICENSE_KEY
${NEW_RELIC_LICENSE_KEY:-9a3465dc990aa65ee1037041a7d0f770ef428cfd}  
ENV NEW_RELIC_LOG ${NEW_RELIC_LOG:-STDOUT}  
  

