FROM jenkins/inbound-agent:alpine as jnlp

FROM node:12.16.1-alpine
USER root

RUN apk -U add openjdk8-jre libcurl curl git

# Install Docker client
ARG DOCKER_VERSION=18.03.0-ce
RUN curl -fsSL https://download.docker.com/linux/static/stable/`uname -m`/docker-$DOCKER_VERSION.tgz | tar --strip-components=1 -xz -C /usr/local/bin docker/docker

COPY --from=jnlp /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-agent
COPY --from=jnlp /usr/share/jenkins/agent.jar /usr/share/jenkins/agent.jar

ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
