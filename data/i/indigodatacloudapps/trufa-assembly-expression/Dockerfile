FROM ubuntu:16.04  
MAINTAINER bhaas@broadinstitute.org  
  
RUN apt-get update && apt-get install -y gcc g++ perl python automake make \  
wget git curl libdb-dev \  
zlib1g-dev bzip2 libncurses5-dev \  
texlive-latex-base \  
default-jre \  
python-pip python-dev \  
gfortran \  
build-essential libghc-zlib-dev libncurses-dev libbz2-dev liblzma-dev
libpcre3-dev libxml2-dev \  
libblas-dev gfortran git unzip ftp libzmq3-dev nano ftp fort77 libreadline-dev
\  
libcurl4-openssl-dev libx11-dev libxt-dev \  
x11-common libcairo2-dev libpng12-dev libreadline6-dev libjpeg8-dev pkg-config
\  
software-properties-common python-setuptools python-dev python-numpy \  
&& apt-get clean  
  
RUN curl -L https://cpanmin.us | perl - App::cpanminus  
  
RUN cpanm install DB_File  
  
RUN cpanm install URI::Escape  
  
## set up tool config and deployment area:  
ENV SRC /usr/local/src  
ENV BIN /usr/local/bin  
  
  
#####  
# Install R  
WORKDIR $SRC  
  
ENV R_VERSION=R-3.3.2  
RUN curl https://cran.r-project.org/src/base/R-3/$R_VERSION.tar.gz -o
$R_VERSION.tar.gz && \  
tar xvf $R_VERSION.tar.gz && \  
cd $R_VERSION && \  
./configure && make && make install  
  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("edgeR", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("DESeq2", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("ape", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("ctc", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("gplots", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("Biobase", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("qvalue", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("goseq", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("Glimma", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("ROTS", dep = TRUE)'  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("GOplot", dep = TRUE)'  
  
## bowtie  
WORKDIR $SRC  
RUN wget https://sourceforge.net/projects/bowtie-
bio/files/bowtie/1.1.2/bowtie-1.1.2-linux-x86_64.zip/download -O
bowtie-1.1.2-linux-x86_64.zip && \  
unzip bowtie-1.1.2-linux-x86_64.zip && \  
cp bowtie-1.1.2/bowtie* $BIN  
  
## RSEM  
RUN mkdir /usr/local/lib/site_perl  
WORKDIR $SRC  
RUN wget https://github.com/deweylab/RSEM/archive/v1.2.31.tar.gz && \  
tar xvf v1.2.31.tar.gz && \  
cd RSEM-1.2.31 && \  
make && \  
cp rsem-* $BIN && \  
cp rsem_perl_utils.pm /usr/local/lib/site_perl/  
  
## Kallisto  
WORKDIR $SRC  
RUN wget
https://github.com/pachterlab/kallisto/releases/download/v0.42.5/kallisto_linux-v0.42.5.tar.gz
&& \  
tar xvf kallisto_linux-v0.42.5.tar.gz && \  
cp kallisto_linux-v0.42.5/kallisto $BIN  
  
## Salmon  
WORKDIR $SRC  
RUN wget https://github.com/COMBINE-
lab/salmon/releases/download/v0.8.0/Salmon-0.8.0_linux_x86_64.tar.gz && \  
tar xvf Salmon-0.8.0_linux_x86_64.tar.gz && \  
ln -s $SRC/Salmon-latest_linux_x86_64/bin/salmon $BIN/.  
  
## FASTQC  
WORKDIR $SRC  
RUN wget
http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip &&
\  
unzip fastqc_v0.11.5.zip && \  
chmod 755 /usr/local/src/FastQC/fastqc && \  
ln -s /usr/local/src/FastQC/fastqc $BIN/.  
  
# blast  
WORKDIR $SRC  
RUN wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.5.0/ncbi-
blast-2.5.0+-x64-linux.tar.gz && \  
tar xvf ncbi-blast-2.5.0+-x64-linux.tar.gz && \  
cp ncbi-blast-2.5.0+/bin/* $BIN  
  
## Bowtie2  
WORKDIR $SRC  
RUN wget https://sourceforge.net/projects/bowtie-
bio/files/bowtie2/2.3.2/bowtie2-2.3.2-linux-x86_64.zip/download -O
bowtie2-2.3.2-linux-x86_64.zip && \  
unzip bowtie2-2.3.2-linux-x86_64.zip && \  
mv bowtie2-2.3.2/bowtie2* $BIN && \  
rm *.zip && \  
rm -r bowtie2-2.3.2  
  
# Install Java.  
RUN \  
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true |
debconf-set-selections && \  
add-apt-repository -y ppa:webupd8team/java && \  
apt-get update && \  
apt-get install -y oracle-java8-installer && \  
rm -rf /var/lib/apt/lists/* && \  
rm -rf /var/cache/oracle-jdk8-installer  
  
#### This is required to install CEGMA  
RUN sed 's/main$/main universe/' -i /etc/apt/sources.list  
RUN apt-get update -y && apt-get upgrade -y  
  
# Install Genewise  
RUN apt-get install -y wise && \  
mkdir -p /opt/genewise && \  
cd /opt/genewise && \  
wget http://korflab.ucdavis.edu/datasets/cegma/wise2.2.3-rc7.tar.gz && \  
tar xfz wise*.tar.gz && \  
rm wise*.tar.gz && \  
ln -s wise2.2.3-rc7 current  
  
# Install HMMER  
RUN apt-get install -y hmmer  
  
# Install geneid  
RUN mkdir -p /opt/geneid && \  
cd /opt/geneid && \  
wget ftp://genome.crg.es/pub/software/geneid/geneid_v1.4.4.Jan_13_2011.tar.gz
&& \  
tar xfz geneid*.tar.gz && \  
rm geneid*.tar.gz && \  
mv geneid current && \  
cd current && \  
make  
  
# Install CEGMA  
ADD http://github.com/KorfLab/CEGMA_v2/archive/v2.5.tar.gz /opt/  
RUN cd /opt/ && \  
tar -xzvf v2.5.tar.gz && \  
mv CEGMA_v2-2.5 cegma && \  
cd cegma && \  
make  
  
ENV WISECONFIGDIR /opt/genewise/current/wisecfg/  
ENV CEGMA /opt/cegma  
ENV PERL5LIB $CEGMA/lib  
ENV PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$CEGMA/bin:/opt/geneid/current/bin/  
  
  
  
##### Install PICARD TOOLS  
RUN git clone \--depth 1 https://github.com/broadinstitute/picard.git
/usr/local/src/picard && \  
cd /usr/local/src/picard && \  
./gradlew shadowJar  
  
# Cleanup  
RUN rm -rf /tmp/picard-tools-*  
##########  
## Trinity  
RUN Rscript -e
'source("http://bioconductor.org/biocLite.R");library(BiocInstaller);
biocLite("argparse", dep = TRUE)'  
  
WORKDIR $SRC  
  
# Version Trinity 2.4.0  
ENV TRINITY_VERSION="2.4.0"  
WORKDIR $SRC  
  
RUN
TRINITY_URL="https://github.com/trinityrnaseq/trinityrnaseq/archive/Trinity-v${TRINITY_VERSION}.tar.gz"
&& \  
wget $TRINITY_URL  
  
RUN tar -xvf Trinity-v${TRINITY_VERSION}.tar.gz  
  
RUN cd trinityrnaseq-Trinity-v${TRINITY_VERSION} && make  
  
ENV TRINITY_HOME $SRC/trinityrnaseq-Trinity-v${TRINITY_VERSION}  
  
RUN cp $TRINITY_HOME/trinity-plugins/BIN/samtools $BIN  
  
ENV PATH=${TRINITY_HOME}:${PATH}  
  
COPY Dockerfile $SRC/Dockerfile.$TRINITY_VERSION  
  
RUN apt-get install -y libtbb-dev && apt-get clean  
  
RUN cd /usr/local/src &&\  
rm -rf *tar.gz  
  
RUN git clone git://github.com/matplotlib/matplotlib.git &&\  
cd matplotlib && \  
python setup.py install  
  
### Install Hisat2  
RUN cd /tmp  
RUN wget
https://launchpad.net/ubuntu/+archive/primary/+files/hisat2_2.0.5.orig.tar.xz  
RUN tar -xvf hisat2_2*tar.xz  
RUN cd hisat2-2.0.5 && make && cp -p hisat2 hisat2-* /usr/bin  
  
#######################################################################  
##Include here the expresssion Docker as well, since it uses Trinity ##  
#######################################################################  
RUN cd /opt && \  
wget http://cole-trapnell-
lab.github.io/cufflinks/assets/downloads/cufflinks-2.2.1.Linux_x86_64.tar.gz
&& \  
tar -zxvf cufflinks-2.2.1*  
ENV PATH="/opt/cufflinks-2.2.1.Linux_x86_64:${PATH}"  
RUN cd /opt && \  
wget
http://bio.math.berkeley.edu/eXpress/downloads/express-1.5.1/express-1.5.1-linux_x86_64.tgz
&& \  
tar -zxvf express-1.5.1-linux_x86_64.tgz  
  
ENV PATH="/opt/express-1.5.1-linux_x86_64:${PATH}"  
#######################################################################  
##################Include the OneData client###########################  
#######################################################################  

