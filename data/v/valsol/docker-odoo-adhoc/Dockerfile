FROM adhoc/odoo-ar:9.0  
MAINTAINER Juan Jose Scarafia <jjs@adhoc.com.ar>  
  
USER root  
  
# Get repositories & add files  
WORKDIR ${RESOURCES}  
COPY ./other-sources.txt ./  
RUN mkdir -p ${EXTRA_ADDONS}  
RUN python get_addons.py ${EXTRA_ADDONS} \--depth=1 \--sources_file=other-
sources.txt  
WORKDIR /  
  
# para pyafipws  
RUN chmod 777 -R /usr/local/lib/python2.7/dist-packages/pyafipws/  
  
# seteamos SERVER_WIDE_MODULES de los modulos incluidos  
ENV SERVER_WIDE_MODULES web,server_mode,database_tools,  
  
USER odoo  

