FROM rubybench/ruby:0.1  
MAINTAINER Guo Xiang "tgx_world@hotmail.com"  
RUN git clone \--verbose --branch trunk --single-branch
https://github.com/shahsaurabh0605/ruby.git  
RUN git clone \--verbose --branch master --single-branch
https://github.com/ruby-bench/ruby-bench-suite.git  
  
ADD runner runner  
ADD config.sub /ruby/tool/config.sub  
ADD config.guess /ruby/tool/config.guess  
RUN chmod 755 runner  
  
CMD /bin/bash -l -c "./runner"  

