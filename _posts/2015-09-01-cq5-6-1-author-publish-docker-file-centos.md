---
layout: post
title: CQ5.6.1 (Author + Publish) Docker file – CentOS
tags:
  - docker
  - adobe cq
comments: true
image:
  path: /images/docker.png
---

<!-- ![_config.yml]({{ site.baseurl }}/images/docker.png) -->

<!--more-->

## Dockerfile

```docker
FROM centos
MAINTAINER vincent

#Install and set java home
RUN mkdir -p /export/apps/jdk
ADD jdk1.7.0_79 /export/apps/jdk/JDK-1_7_0_79
ENV JAVA_HOME /export/apps/jdk/JDK-1_7_0_79
ENV PATH $PATH:$JAVA_HOME/bin

#Install CQ Author
RUN mkdir -p /export/apps/aem/author
WORKDIR /export/apps/aem/author
ADD cq5-author-p4502.jar /export/apps/aem/author/cq5-author-p4502.jar
ADD license.properties /export/apps/aem/author/license.properties
RUN java -jar cq5-author-p4502.jar -unpack -v

#Now start Publish Instance
RUN mkdir -p /export/apps/aem/publish
WORKDIR /export/apps/aem/publish
ADD cq5-author-p4502.jar /export/apps/aem/publish/cq5-publish-p4503.jar
ADD license.properties /export/apps/aem/publish/license.properties
RUN java -jar cq5-publish-p4503.jar -unpack -v

#Set up all CQ ENV
ENV CQ_FOREGROUND y
ENV CQ_VERBOSE y
ENV CQ_NOBROWSER y
ENV CQ_RUNMODE “author,publish”
ENV CQ_JVM_OPTS “-server -Xmx1524M -Xms512M -XX:MaxPermSize=512M”

RUN yum install -y epel-release && \
yum install -y supervisor && \
yum clean all
EXPOSE 80 443 4502 4503
```

## Run multiple process in same docker image

```docker
RUN echo “[supervisord]” > /etc/supervisord.conf && \
echo “nodaemon=true” >> /etc/supervisord.conf && \
echo “” >> /etc/supervisord.conf && \
echo “[program:aem_author]” >> /etc/supervisord.conf && \
echo “startsecs = 0” >> /etc/supervisord.conf && \
echo “autorestart = false” >> /etc/supervisord.conf && \
echo “command=/export/apps/aem/author/crx-quickstart/bin/start” >> /etc/supervisord.conf && \
echo “” >> /etc/supervisord.conf && \
echo “[program:aem_publish]” >> /etc/supervisord.conf && \
echo “startsecs = 0” >> /etc/supervisord.conf && \
echo “autorestart = false” >> /etc/supervisord.conf && \
echo “command=/export/apps/aem/publish/crx-quickstart/bin/start” >> /etc/supervisord.conf
CMD [“/usr/bin/supervisord”]

```

Happy Coding! 😇
