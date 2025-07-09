FROM curlimages/curl:latest as build

ENV MULE_VERSION=4.5.0

RUN set -eux; \
    curl \
        https://repository-master.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/${MULE_VERSION}/mule-standalone-${MULE_VERSION}.tar.gz \
        -o /home/curl_user/mule-standalone-${MULE_VERSION}.tar.gz; \
        tar xzf /home/curl_user/mule-standalone-${MULE_VERSION}.tar.gz

FROM eclipse-temurin:8
LABEL   com.bmeme.project.family='Mule Standalone Docker Image' \
        com.bmeme.project.version='4.5.0-8' \
        com.bmeme.maintainer.1='Daniele Piaggesi <daniele.piaggesi@bmeme.com>' \
        com.bmeme.maintainer.2='Roberto Mariani <roberto.mariani@bmeme.com>' \
        com.bmeme.refreshedat='2025-07-09'

ENV MULE_HOME=/opt/mule
ENV MULE_USER=mule
ENV MULE_VERSION=4.5.0
ENV TZ=Europe/Rome

COPY --from=build /home/curl_user/mule-standalone-${MULE_VERSION} ${MULE_HOME}

RUN set -eux; \
    echo ${TZ} > /etc/timezone; \
    existing_user=$(getent passwd 1000 | cut -d: -f1 || true); \
    if [ -n "$existing_user" ]; then \
        userdel -r "$existing_user" || true; \
    fi; \
    groupadd -g 1000 ${MULE_USER}; \
    useradd -m -d ${MULE_HOME} -u 1000 -g 1000 -s /usr/sbin/nologin ${MULE_USER}; \
    chown -R ${MULE_USER}:${MULE_USER} ${MULE_HOME}

# Define working directory.
USER ${MULE_USER}
WORKDIR ${MULE_HOME}

CMD [ "/opt/mule/bin/mule"]

# Default http port
EXPOSE 8081
