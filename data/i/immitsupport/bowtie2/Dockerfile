FROM ubuntu:16.04  
MAINTAINER André Fragoso <andre.fragoso@medicina.ulisboa.pt>  
  
##############################################################  
# Software: bowtie  
# Software Version: 2.2.6  
# Software Website: https://github.com/BenLangmead/bowtie2  
# Description: bowtie2  
##############################################################  
  
#INSTALL DEPENDENCIES & CLEAN UP REPOSITORY  
  
RUN apt-get update && \  
apt-get install -y \  
curl \  
zip \  
samtools \  
python &&\  
rm -rf /var/lib/apt/lists/* && \  
apt-get clean autoclean && \  
apt-get autoremove -y  
  
#SET WORKDIR ENV  
  
WORKDIR /bowtie2/  
ENV work_dir="/bowtie2/bowtie2-2.2.6"  
  
#DOWNLOAD & EXTRACT BOWTIE2  
  
RUN curl -L \  
"http://downloads.sourceforge.net/project/bowtie-
bio/bowtie2/2.2.6/bowtie2-2.2.6-linux-x86_64.zip?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fbowtie-
bio%2Ffiles%2Fbowtie2%2F2.2.6%2F&ts=1451933812&use_mirror=skylineservers" \  
> bowtie2-2.2.6-linux-x86_64.zip &&\  
unzip bowtie2-2.2.6-linux-x86_64.zip &&\  
rm bowtie2-2.2.6-linux-x86_64.zip  
  
ENV PATH="${work_dir}:${PATH}"  
  
RUN bowtie2 --help  

