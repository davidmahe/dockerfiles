FROM phusion/baseimage  
  
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle \  
ANDROID_HOME=/opt/android-sdk \  
PATH="$PATH:/usr/lib/jvm/java-8-oracle/bin:/opt/android-
sdk/tools:/opt/android-sdk/platform-tools"  
RUN apt-get update -qq  
RUN apt-get install -y --no-install-recommends wget lib32stdc++6
libqt5widgets5 lib32z1 unzip  
RUN apt-get install -y awscli  
RUN apt-get install -y expect  
  
###################  
# JDK8  
###################  
RUN \  
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true |
debconf-set-selections && \  
add-apt-repository -y ppa:webupd8team/java && \  
apt-get update && \  
apt-get install -y oracle-java8-installer && \  
rm -rf /var/lib/apt/lists/* && \  
rm -rf /var/cache/oracle-jdk8-installer  
RUN java -version  
  
##################  
# Android licenses  
##################  
RUN mkdir /opt/android-sdk/  
RUN mkdir /opt/android-sdk/licenses/  
RUN echo "8933bad161af4178b1185d1a37fbf41ea5269c55" > /opt/android-
sdk/licenses/android-sdk-license  
RUN echo "84831b9409646a918e30573bab4c9c91346d8abd" > /opt/android-
sdk/licenses/android-sdk-preview-license  
RUN echo "d975f751698a77b662f1254ddbeed3901e976f5a" > /opt/android-
sdk/licenses/intel-android-extra-license  
  
###################  
# Android SDK  
###################  
RUN wget -O android-sdk.zip
https://dl.google.com/android/repository/tools_r25.2.3-linux.zip  
RUN unzip -a android-sdk.zip  
RUN rm android-sdk.zip  
RUN mv /tools /opt/android-sdk/tools  
RUN echo $ANDROID_HOME  
RUN echo $PATH  
RUN ls -al /opt  
RUN ls -al /opt/android-sdk  
RUN ls -al /opt/android-sdk/tools  
RUN echo 'y' | android update sdk --no-ui -a --filter platform-tools,build-
tools-25.0.2,android-25,extra-android-support,extra-google-support,extra-
google-google_play_services,extra-google-m2repository,extra-
android-m2repository --force  
RUN rm -rf /opt/android-sdk/add-ons  
  
##################  
# Speeding up android builds  
# Gradle will pick these properties when running  
##################  
RUN mkdir ~/.gradle  
RUN echo "org.gradle.daemon=true" >> ~/.gradle/gradle.properties  
RUN echo "org.gradle.jvmargs=-Xmx4096m -XX:MaxPermSize=512m
-XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8" >>
~/.gradle/gradle.properties  
RUN echo "org.gradle.parallel=true" >> ~/.gradle/gradle.properties  
RUN echo "org.gradle.configureondemand=true" >> ~/.gradle/gradle.properties  
RUN echo "android.builder.sdkDownload=true" >> ~/.gradle/gradle.properties  
RUN rm -rf /var/lib/apt/lists/*  

