FROM ruby:2.4-alpine

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
    echo '#!/bin/sh'; \
    echo 'set -e'; \
    echo; \
    echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
  } > /usr/local/bin/docker-java-home \
  && chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u111
ENV JAVA_ALPINE_VERSION 8.111.14-r0

RUN set -x \
  && apk add --no-cache \
    openjdk8="$JAVA_ALPINE_VERSION" \
    openssl \
  && [ "$JAVA_HOME" = "$(docker-java-home)" ]

ARG S2M_VERSION="1.3.1" 

RUN gem install asciidoctor
RUN mkdir /html-convertor && wget -O /html-convertor/swagger2markup-cli.jar  https://jcenter.bintray.com/io/github/swagger2markup/swagger2markup-cli/${S2M_VERSION}/swagger2markup-cli-${S2M_VERSION}.jar
