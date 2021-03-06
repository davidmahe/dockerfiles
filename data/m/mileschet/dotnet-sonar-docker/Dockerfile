FROM buildpack-deps:jessie-scm  
  
# Install .NET CLI dependencies  
RUN apt-get update \  
&& apt-get install -y --no-install-recommends \  
libc6 \  
libcurl3 \  
libgcc1 \  
libgssapi-krb5-2 \  
libicu52 \  
liblttng-ust0 \  
libssl1.0.0 \  
libstdc++6 \  
libunwind8 \  
libuuid1 \  
zlib1g \  
unzip \  
&& rm -rf /var/lib/apt/lists/*  
  
# Install .NET Core SDK  
ENV DOTNET_SDK_VERSION 2.0.0-preview2-006497  
ENV DOTNET_SDK_DOWNLOAD_URL
https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-
sdk-$DOTNET_SDK_VERSION-linux-x64.tar.gz  
ENV DOTNET_SDK_DOWNLOAD_SHA
0664FE726EB07650D9C036B0E5E6D33AA8B10DB89DADA4A5E85FB5757FD1FAE1570AF0D526484014976761C829B1E55A70EF9966EECE877A56C2C426090896EB  
  
ENV SONAR_RUNNER_URL https://sonarsource.bintray.com/Distribution/sonar-
scanner-cli/sonar-scanner-cli-3.0.3.778-linux.zip  
  
RUN curl -SL $DOTNET_SDK_DOWNLOAD_URL --output dotnet.tar.gz \  
&& echo "$DOTNET_SDK_DOWNLOAD_SHA dotnet.tar.gz" | sha512sum -c - \  
&& mkdir -p /usr/share/dotnet \  
&& tar -zxf dotnet.tar.gz -C /usr/share/dotnet \  
&& rm dotnet.tar.gz \  
&& ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet  
  
# Trigger the population of the local package cache  
ENV NUGET_XMLDOC_MODE skip  
RUN mkdir warmup \  
&& cd warmup \  
&& dotnet new \  
&& cd .. \  
&& rm -rf warmup \  
&& rm -rf /tmp/NuGetScratch  
  
# Install  
RUN curl -SL $SONAR_RUNNER_URL --output sonar-scanner.zip \  
&& unzip -d /usr/share/ sonar-scanner.zip \  
&& ln -s /usr/share/sonar-scanner-3.0.3.778-linux/bin/sonar-scanner
/usr/bin/sonar-scanner  
  
  

