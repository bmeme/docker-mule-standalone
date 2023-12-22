FROM curlimages/curl:latest as build

ENV MULE_VERSION=4.4.0

RUN set -eux; \
    curl \
        https://repository-master.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/${MULE_VERSION}/mule-standalone-${MULE_VERSION}.tar.gz \
        -o /home/curl_user/mule-standalone-${MULE_VERSION}.tar.gz; \
        tar xzf /home/curl_user/mule-standalone-${MULE_VERSION}.tar.gz

FROM eclipse-temurin:11
LABEL   com.bmeme.project.family='Mule Standalone Docker Image' \
        com.bmeme.project.version='4.4.0-11' \
        com.bmeme.maintainer.1='Daniele Piaggesi <daniele.piaggesi@bmeme.com>' \
        com.bmeme.maintainer.2='Roberto Mariani <roberto.mariani@bmeme.com>' \
        com.bmeme.refreshedat='2023-11-22'

ENV MULE_HOME=/opt/mule
ENV MULE_USER=mule
ENV MULE_VERSION=4.4.0
ENV TZ=Europe/Rome

COPY --from=build /home/curl_user/mule-standalone-${MULE_VERSION} ${MULE_HOME}

RUN set -eux; \
    echo ${TZ} > /etc/timezone; \
    \
    # Create Mule Standalone user
    groupadd ${MULE_USER}; \
    useradd -g ${MULE_USER} -d ${MULE_HOME} -s /usr/sbin/nologin ${MULE_USER}; \
    chown -R ${MULE_USER}:${MULE_USER} ${MULE_HOME}

# Define working directory.
USER ${MULE_USER}
WORKDIR ${MULE_HOME}

CMD [ "/opt/mule/bin/mule"]

# Default http port
EXPOSE 8081
