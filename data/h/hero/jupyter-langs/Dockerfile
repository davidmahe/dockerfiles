# jupyter-langs:all  
# VERSION 1.3.1  
FROM hero/jupyter-langs:zeromq  
  
# Install SPARQL  
RUN pip install sparqlkernel && \  
jupyter sparqlkernel install  
  
# Install R  
RUN conda install --quiet --yes \  
'r-base' \  
'r-irkernel' \  
'r-plyr' \  
'r-devtools' \  
'r-tidyverse' \  
'r-shiny' \  
'r-rmarkdown' \  
'r-forecast' \  
'r-rsqlite' \  
'r-reshape2' \  
'r-nycflights13' \  
'r-caret' \  
'r-rcurl' \  
'r-crayon' \  
'r-randomforest' \  
'r-tensorflow' \  
&& conda clean -tipsy  
  
# Install Javascript  
ENV NODE_VERSION=8.9.0  
RUN git clone https://github.com/riywo/ndenv $HOME/.ndenv && \  
mkdir -p $HOME/.ndenv/plugins && \  
git clone https://github.com/riywo/node-build.git $HOME/.ndenv/plugins/node-
build && \  
git clone https://github.com/pine/ndenv-yarn-install.git
$HOME/.ndenv/plugins/ndenv-yarn-install && \  
echo 'export PATH="$HOME/.ndenv/bin:$PATH"' >> $HOME/.bashrc && \  
echo 'eval "$(ndenv init -)"' >> $HOME/.bashrc  
ENV PATH=$HOME/.ndenv/bin:$HOME/.ndenv/shims:$PATH  
RUN ndenv install $NODE_VERSION && \  
ndenv global $NODE_VERSION  
RUN eval "$(ndenv init -)" && \  
yarn global add ijavascript jp-babel && \  
ijsinstall && \  
jp-babel-install  
  
# Install Ruby  
ENV RUBY_VERSION=2.4.2  
RUN apt-get update && \  
apt-get install -y --no-install-recommends \  
gsl-bin \  
libgsl0-dev \  
&& rm -rf /var/lib/apt/lists/*  
  
RUN git clone https://github.com/rbenv/rbenv.git $HOME/.rbenv && \  
mkdir -p $HOME/.rbenv/plugins && \  
git clone https://github.com/rbenv/ruby-build.git $HOME/.rbenv/plugins/ruby-
build && \  
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> $HOME/.bashrc && \  
echo 'eval "$(rbenv init -)"' >> $HOME/.bashrc  
ENV PATH=$HOME/.rbenv/bin:$HOME/.rbenv/shims:$PATH  
RUN rbenv install $RUBY_VERSION && \  
rbenv global $RUBY_VERSION  
RUN eval "$(rbenv init -)"  
RUN LD_LIBRARY_PATH=/usr/local/lib \  
gem install --no-ri --no-rdoc \  
cztop \  
sciruby \  
daru \  
nyaplot \  
#sciruby-full \  
bundler \  
iruby  
RUN iruby register --force  

