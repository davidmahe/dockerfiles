FROM ubuntu:16.04 as build  
  
RUN mkdir /app  
RUN mkdir /build  
WORKDIR /build  
  
COPY build/scripts/install_build_dependencies
/app/build/scripts/install_build_dependencies  
COPY build/package_dependencies.sh /app/build/package_dependencies.sh  
RUN /app/build/scripts/install_build_dependencies  
  
COPY build/scripts/download_cmake /app/build/scripts/download_cmake  
RUN /app/build/scripts/download_cmake  
  
COPY CMakeLists.txt /app/CMakeLists.txt  
COPY build/cmake/functions /app/build/cmake/functions  
COPY build/cmake/deps /app/build/cmake/deps  
COPY build/cmake/deps.cmake /app/build/cmake/deps.cmake  
COPY build/patches /app/build/patches  
COPY configure /app/configure  
RUN /app/configure && make deps  
  
COPY build/cmake/build-deps /app/build/cmake/build-deps  
COPY build/cmake/build-deps.cmake /app/build/cmake/build-deps.cmake  
RUN /app/configure && make build-deps  
  
COPY build/cmake/app-deps /app/build/cmake/app-deps  
COPY build/cmake/app-deps.cmake /app/build/cmake/app-deps.cmake  
RUN /app/configure && make app-deps  
  
COPY . /app  
RUN /app/configure && make  
RUN make package  
  
FROM ubuntu:16.04  
COPY \--from=build /build/build/package/work/build/core /tmp/package  
RUN apt-get update && \  
apt-get -y install gdebi-core && \  
gdebi --non-interactive /tmp/package/*.deb && \  
apt-get -y --purge remove gdebi-core && \  
apt-get -y --purge autoremove && \  
rm -rf /tmp/package /var/lib/apt/lists/*  
  
CMD ["api-umbrella", "run"]  

