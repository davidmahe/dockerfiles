#################################################################  
# Dockerfile  
#  
# Software: Super Enhancer  
# Software Version: 1a9bb86b5464  
# Description: Super Enhancer Image for Scidap  
# Website: https://bitbucket.org/young_computation/rose, http://scidap.com/  
# Provides: https://bitbucket.org/young_computation/rose/get/1a9bb86b5464.zip  
# Base Image: scidap/scidap:v0.0.1  
# Build Cmd: docker build --rm -t scidap/superenhancer .  
# Pull Cmd: docker pull scidap/superenhancer  
# Run Cmd: docker run --rm scidap/superenhancer  
#################################################################  
  
FROM scidap/samtools:v1.2-242-4d56437  
MAINTAINER BHARATH MANICKA VASAGAM bharath.manickavasagam@cchmc.org  
ENV DEBIAN_FRONTEND noninteractive  
  
################## BEGIN INSTALLATION ######################  
  
  
WORKDIR /usr/local/bin/  
  
### Install required packages  
#To configure the virtualbox with another DNS  
#CMD "sh" "-c" "echo nameserver 8.8.8.8 > /etc/resolv.conf"  
#change the nameserver in resolv.conf to current DNS server  
  
RUN rm -rf /var/lib/apt/lists/* && \  
apt-get clean all && \  
apt-get update && \  
apt-get install -y \  
libncurses5-dev \  
ed \  
less \  
locales \  
wget \  
r-base \  
ca-certificates && \  
apt-get clean && \  
apt-get purge && \  
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
/var/lib/apt/lists/*  
  
### Patch File  
  
RUN echo '--- ROSE_bamToGFF.py\n\  
+++ ROSE_bamToGFF.py\n\  
74c74\n\  
< gffLocus =
ROSE_utils.Locus(line[0],int(line[3]),int(line[4]),line[6],line[1])\n\  
\---\n\  
> gffLocus =
ROSE_utils.Locus(line[0],float(line[3]),float(line[4]),line[6],line[1])\n\  
\--- ROSE_main.py\n\  
+++ ROSE_main.py\n\  
241c241\n\  
< usage = "usage: %prog [options] -g [GENOME] -i [INPUT_REGION_GFF] -r
[RANKBY_BAM_FILE] -o [OUTPUT_FOLDER] [OPTIONAL_FLAGS]"\n\  
\---\n\  
> usage = "usage: %prog [options] -g [INPUT_GENOME] -i [INPUT_REGION_GFF] -r
[RANKBY_BAM_FILE] -o [OUTPUT_FOLDER] [OPTIONAL_FLAGS]"\n\  
251c251\n\  
< help = "Enter the genome build (MM9,MM8,HG18,HG19)")\n\  
\---\n\  
> help = "Reference genome file: example- hg18_refseq.ucsc")\n\  
301a302\n\  
> \n\  
332c333\n\  
< \n\  
\---\n\  
> \'\  
>> patch.diff  
  
RUN echo "336,342c337,345\n\  
< genomeDict = {\n\  
< 'HG18':'%s/annotation/hg18_refseq.ucsc' % (cwd),\n\  
< 'MM9': '%s/annotation/mm9_refseq.ucsc' % (cwd),\n\  
< 'HG19':'%s/annotation/hg19_refseq.ucsc' % (cwd),\n\  
< 'MM8': '%s/annotation/mm8_refseq.ucsc' % (cwd),\n\  
< 'MM10':'%s/annotation/mm10_refseq.ucsc' % (cwd),\n\  
< }\n\  
\---\n\  
> ## genomeDict = {\n\  
> ## 'HG18':'%s/annotation/hg18_refseq.ucsc' % (cwd),\n\  
> ## 'MM9': '%s/annotation/mm9_refseq.ucsc' % (cwd),\n\  
> ## 'HG19':'%s/annotation/hg19_refseq.ucsc' % (cwd),\n\  
> ## 'MM8': '%s/annotation/mm8_refseq.ucsc' % (cwd),\n\  
> ## 'MM10':'%s/annotation/mm10_refseq.ucsc' % (cwd),\n\  
> ## }\n\  
> \n\  
> annotFile = genome\n\  
344c347\n\  
< annotFile = genomeDict[upper(genome)]\n\  
\---\n\  
> ## annotFile = genomeDict[upper(genome)]\n\  
412c415"\  
>> patch.diff  
RUN echo '< cmd1 = "python ROSE_bamToGFF.py -f 1 -e 200 -r -m %s -b %s -i %s
-o %s &" % (nBin,bamFile,stitchedGFFFile,mappedOut1)\n\  
\---\n\  
> cmd1 = "python /usr/local/'bin'/ROSE_bamToGFF.py -f 1 -e 200 -r -m %s -b %s
-i %s -o %s &" % (nBin,bamFile,stitchedGFFFile,mappedOut1)\n\  
419c422\n\  
< cmd2 = "python ROSE_bamToGFF.py -f 1 -e 200 -r -m %s -b %s -i %s -o %s &" %
(nBin,bamFile,inputGFFFile,mappedOut2)\n\  
\---\n\  
> cmd2 = "python /usr/local/'bin'/ROSE_bamToGFF.py -f 1 -e 200 -r -m %s -b %s
-i %s -o %s &" % (nBin,bamFile,inputGFFFile,mappedOut2)\n\  
484c487\'\  
>> patch.diff  
RUN echo "< cmd = 'R --no-save %s %s %s %s < ROSE_callSuper.R' %
(outFolder,outputFile1,inputName,controlName)\n\  
\---\n\  
> cmd = 'R --no-save %s %s %s %s < /usr/local/bin/ROSE_callSuper.R' %
(outFolder,outputFile1,inputName,controlName)\n\  
489c492\n\  
< cmd = 'R --no-save %s %s %s %s < ROSE_callSuper.R' %
(outFolder,outputFile1,inputName,controlName)\n\  
\---\n\  
> cmd = ‘R --no-save %s %s %s %s < /usr/local/bin/ROSE_callSuper.R' %
(outFolder,outputFile1,inputName,controlName)\n\  
\--- ROSE_utils.py\n\  
+++ ROSE_utils.py\n\  
265c265\n\  
< coords = [int(start),int(end)]\n\  
\---\n\  
> coords = [float(start),float(end)]\n"\  
>> patch.diff  
  
RUN cat patch.diff  
  
### patching the difference in script  
RUN wget -q -O young_computation.zip
https://bitbucket.org/young_computation/rose/get/1a9bb86b5464.zip && \  
unzip young_computation.zip && \  
rm -f young_computation.zip && \  
rm -rf /usr/local/bin/young_computation-rose-1a9bb86b5464/annotation && \  
cp -r young_computation-rose-1a9bb86b5464/* /usr/local/bin && \  
patch < patch.diff && \  
rm patch.diff && \  
rm -rf young_computation-rose-1a9bb86b5464 && \  
rm -f /usr/local/edited-Super-Enhancer-master.zip && \  
chmod -R +x /usr/local/bin  

