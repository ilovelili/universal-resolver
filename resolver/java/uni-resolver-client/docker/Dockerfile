# Dockerfile for universalresolver/uni-resolver-client

FROM maven:3-jdk-8
MAINTAINER Markus Sabadello <markus@danubetech.com>

USER root

# install dependencies

ARG GITHUB_READ_PACKAGES_OWNER
ARG GITHUB_READ_PACKAGES_TOKEN
ADD ./resolver/java/settings.xml /root/.m2/

# build dependencies

RUN cd /opt/ && git clone https://github.com/decentralized-identity/did-common-java.git && \
    cd /opt/did-common-java/ && mvn clean install -DskipTests

# build uni-resolver-client

ADD ./resolver/java/ /opt/uni-resolver-java

RUN cd /opt/uni-resolver-java && mvn clean install -N -DskipTests && mvn clean && \
    cd /opt/uni-resolver-java/uni-resolver-core && mvn clean install -N -DskipTests && mvn clean && \
    cd /opt/uni-resolver-java/uni-resolver-client && mvn clean install -N -DskipTests && mvn clean
