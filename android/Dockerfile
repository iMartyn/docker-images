# Image pubnative/android

FROM centos

MAINTAINER Eros Garcia Ponte <eros902002@googlemail.com>

WORKDIR /usr/local/

# Install Development Tools
RUN yum -y groupinstall "Development Tools"

# yum update
RUN yum -y update

# Install Java 1.8 in CentOS/RHEL 7.X
RUN cd /usr/local/ \
 && curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm > jdk-8u131-linux-x64.rpm \
 && yum -y localinstall jdk-8u131-linux-x64.rpm

RUN ls /usr/java
#RUN java -version
#RUN find /usr/java -wholename '*ava/jdk*' -prune

# Java environment variables
ENV JAVA_VERSION 1.8
ENV JAVA_HOME /usr/java/jdk1.8.0_131
ENV JRE_HOME /usr/java/jdk1.8.0_131/jre
ENV PATH $PATH:/usr/java/jdk1.8.0_131/bin:/usr/java/jdk1.8.0_131/jre/bin

# Install 32bit Library
RUN yum -y install glibc.i686 \
                   libstdc++.i686 \
                   glibc-devel.i686 \
                   zlib-devel.i686 \
                   ncurses-devel.i686 \
                   libX11-devel.i686 \
                   libXrender.i686

# Install Android SDK
RUN mkdir -p /usr/local/android-sdk \
 && cd /usr/local/android-sdk \
 && curl -L -O https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
 && ls -la \
 && unzip sdk-tools-linux-3859397.zip

RUN cd /usr/local/ && ls -la

# Install Android tools
RUN /usr/local/android-sdk/tools/bin/sdkmanager --update <<< 'y'
RUN yes | /usr/local/android-sdk/tools/bin/sdkmanager "platforms;android-26" "build-tools;26.0.2" "extras;google;m2repository" "extras;android;m2repository"
#RUN echo yes | /usr/local/android-sdk-linux/tools/android update sdk --filter android-26 --no-ui --force -a
#RUN echo yes | /usr/local/android-sdk-linux/tools/android update sdk --filter platform-tools --no-ui --force -a
#RUN echo yes | /usr/local/android-sdk-linux/tools/android update sdk --filter tools --no-ui --force -a
#RUN echo yes | /usr/local/android-sdk-linux/tools/android update sdk --filter extra --no-ui --force -a

RUN cd /usr/local/ && ls -la

# Environment variables
ENV ANDROID_HOME /usr/local/android-sdk
ENV JAVA_VERSION 1.8
ENV JAVA_HOME /usr/java/jdk1.8.0_131
ENV JRE_HOME /usr/java/jdk1.8.0_131/jre
ENV PATH $PATH:/usr/java/jdk1.8.0_131/bin:/usr/java/jdk1.8.0_131/jre/bin
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANT_HOME/bin

# Clean up
RUN yum clean all
RUN rm -rf /usr/local/sdk-tools-linux-3859397.zip /usr/local/jdk-8u131-linux-x64.rpm /var/cache/yum
