FROM informaticsmatters/rdkit:Release_2017_09_1  
LABEL maintainer="Tim Dudgeon<tdudgeon@informaticsmatters.com>"  
  
USER root  
  
# install pipelines python modules  
RUN apt-get -y update && apt-get install -y --no-install-recommends python-
setuptools  
  
# Copy the pipeline implementation into the image  
COPY src/python /opt/python  
RUN pip install -e /opt/python  
# And the pipeline-utilities  
RUN pip install matplotlib im-pipelines-utils==2.2.* im-pipelines-utils-
rdkit==1.4.*  

