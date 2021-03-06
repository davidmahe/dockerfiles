FROM rocker/r-devel:latest  
  
# RUN echo "deb http://ftp.debian.org/debian experimental main" >
/etc/apt/sources.list.d/debian-experimental.list  
RUN apt-get update -qq \  
&& apt-get install -t unstable -y \  
automake \  
clang-3.7 \  
cmake \  
curl \  
fonts-inconsolata \  
git \  
libcurl4-openssl-dev \  
libssh2-1-dev \  
libssl-dev \  
libxml2-dev \  
pandoc \  
pandoc-citeproc \  
qpdf \  
texlive-base \  
&& apt-get clean  
  
WORKDIR /usr/local/src  
  
## Check out R-devel  
RUN svn co http://svn.r-project.org/R/trunk R-devel  
  
# SVN R-devel doesn't always compile. An alternative is to grab the devel tar:  
# https://stat.ethz.ch/R/daily/R-devel.tar.bz2 but this is just a svn snap
which may not compile either  
#  
# the following is a rc version, and appears to be attached to a revision of
SVN repo which is not the latest (and thus suggests it is more likely to
compile) Temporarily use this instead of SVN  
# RUN rm -rf /tmp/R-devel \  
# && cd /tmp \  
# && curl https://cran.rstudio.com/src/base-prerelease/R-latest.tar.gz | tar
xz \  
# # move rc to devel so i can switch back to svn easily  
# && mv /tmp/R-rc /tmp/R-devel  
# perhaps prefer a 3.8 branch here, not always trunk.  
# it will be llvm-project/*/tags/RELEASE_380/final or rc2 instead of final  
RUN svn co https://llvm.org/svn/llvm-project/llvm/trunk llvm  
RUN svn co https://llvm.org/svn/llvm-project/cfe/trunk clang  
RUN svn co https://llvm.org/svn/llvm-project/clang-tools-extra/trunk clang-
tools-extra  
RUN svn co https://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt  
RUN svn co https://llvm.org/svn/llvm-project/libcxx/trunk libcxx  
RUN svn co https://llvm.org/svn/llvm-project/libcxxabi/trunk libcxxabi  
RUN svn co http://llvm.org/svn/llvm-project/openmp/trunk openmp  
  
RUN mv clang llvm/tools  
RUN mv compiler-rt llvm/projects  
RUN mv clang-tools-extra llvm/tools/clang/tools  
RUN mv libcxx llvm/projects  
RUN mv libcxxabi llvm/projects  
RUN mv openmp llvm/projects  
  
RUN mkdir llvm-build \  
&& cd llvm-build && \  
cmake \  
-DCMAKE_BUILD_TYPE:STRING=Release \  
-DLLVM_TARGETS_TO_BUILD:STRING=host \  
-DCMAKE_INSTALL_PREFIX=/usr/local \  
-DCLANG_DEFAULT_OPENMP_RUNTIME:STRING=libomp \  
../llvm \  
&& make -j5 \  
&& make install \  
&& cd \  
&& rm -rf llvm-build \  
&& ldconfig  
  
# use config.site to set the R build environment  
COPY config.site /tmp/R-devel/config.site  
RUN ./configure \  
\--enable-R-shlib \  
\--without-blas \  
\--without-lapack \  
\--with-readline \  
\--without-recommended-packages \  
\--program-suffix=devsan \  
&& make \  
&& make install \  
&& make clean \  
&& rm -rf /usr/local/src/R-devel  
  
## Set Renviron to get libs from base R install  
RUN echo "R_LIBS=\${R_LIBS-'/usr/local/lib/R/site-
library:/usr/local/lib/R/library:/usr/lib/R/library'}" >>
/usr/local/lib/R/etc/Renviron  
  
## Set default CRAN repo  
RUN echo 'options("repos"="https://cran.rstudio.com")' >>
/usr/local/lib/R/etc/Rprofile.site  
  
# R doesn't actually run at all without this (can be considered a test of
whether the sanitizers were actually compiled in correctly!)  
ENV ASAN_OPTIONS 'detect_leaks=0:detect_odr_violation=0'  

