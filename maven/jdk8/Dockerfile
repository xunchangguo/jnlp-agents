FROM jenkins/inbound-agent:alpine as jnlp

FROM maven:3.6.1-jdk-8-slim
USER root

RUN apt-get update && \
    apt-get install -y \
        git \
        libfontconfig1 \
        libfreetype6

# Install Docker client
ARG DOCKER_VERSION=18.03.0-ce
RUN curl -fsSL https://download.docker.com/linux/static/stable/`uname -m`/docker-$DOCKER_VERSION.tgz | tar --strip-components=1 -xz -C /usr/local/bin docker/docker

COPY --from=jnlp /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-agent
COPY --from=jnlp /usr/share/jenkins/agent.jar /usr/share/jenkins/agent.jar

ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
