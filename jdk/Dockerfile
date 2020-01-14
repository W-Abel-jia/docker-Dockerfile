FROM debian:latest

ARG DIR_JAVA_BASE=/usr/local/share/java
ARG DIR_JAVA_HOME=${DIR_JAVA_BASE}/jdk1.8.0_231
ARG VER_MAVEN=3.2.5
ARG MAVEN_DOWNLOAD_URL=https://apache.osuosl.org/maven/maven-3/${VER_MAVEN}/binaries
ARG DIR_MAVEN_BASE=/usr/local/share/maven
ARG USER_HOME_DIR="/root"

COPY jdk-8u231-linux-x64.tar.gz /tmp

RUN apt-get update && apt-get install upgrade && apt-get install -y locales && apt-get -y install curl && rm -rf /var/lib/apt/lists/* \
    && localedef -i zh_CN -c -f UTF-8 -A /usr/share/locale/locale.alias zh_CN.UTF-8

ENV LANG zh_CN.UTF-8

RUN mkdir -p ${DIR_MAVEN_BASE} ${DIR_JAVA_HOME} && \
    tar -xvf /tmp/jdk-8u231-linux-x64.tar.gz -C ${DIR_JAVA_BASE} && \
    curl -fsSL -o /tmp/apache-maven.tar.gz ${MAVEN_DOWNLOAD_URL}/apache-maven-${VER_MAVEN}-bin.tar.gz &&\
    tar -xzf /tmp/apache-maven.tar.gz -C ${DIR_MAVEN_BASE} --strip-components=1 &&\
    rm -f /tmp/apache-maven.tar.gz /tmp/jdk-8u231-linux-x64.tar.gz &&\
    ln -s ${DIR_MAVEN_BASE}/bin/mvn /usr/bin/mvn

ENV JAVA_HOME ${DIR_JAVA_HOME}
ENV PATH $PATH:${DIR_JAVA_HOME}/bin
ENV MAVEN_HOME   ${DIR_MAVEN_BASE}
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"


COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["java"]
