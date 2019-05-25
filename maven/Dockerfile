FROM centos:7.5-base

ARG DIR_JAVA_BASE=/usr/local/share/java
ARG DIR_JAVA_HOME=${DIR_JAVA_BASE}/jdk1.6.0_45
ARG VER_MAVEN=3.2.5
ARG MAVEN_DOWNLOAD_URL=https://apache.osuosl.org/maven/maven-3/${VER_MAVEN}/binaries
ARG DIR_MAVEN_BASE=/usr/local/share/maven
ARG USER_HOME_DIR="/root"

COPY jdk-6u45.tar.gz /tmp

RUN mkdir -p ${DIR_MAVEN_BASE} ${DIR_JAVA_HOME} && \
    tar xvf /tmp/jdk-6u45.tar.gz -C ${DIR_JAVA_BASE} && \
    curl -fsSL -o /tmp/apache-maven.tar.gz ${MAVEN_DOWNLOAD_URL}/apache-maven-${VER_MAVEN}-bin.tar.gz &&\
    tar -xzf /tmp/apache-maven.tar.gz -C ${DIR_MAVEN_BASE} --strip-components=1 &&\
    rm -f /tmp/apache-maven.tar.gz /tmp/jdk-6u45.tar.gz &&\
    ln -s ${DIR_MAVEN_BASE}/bin/mvn /usr/bin/mvn

ENV JAVA_HOME ${DIR_JAVA_HOME}
ENV PATH $PATH:${DIR_JAVA_HOME}/bin
ENV MAVEN_HOME   ${DIR_MAVEN_BASE}
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"
ENV LANG         zh_CN.UTF-8

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
