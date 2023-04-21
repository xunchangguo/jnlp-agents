FROM jenkins/inbound-agent:alpine-jdk8 as jnlp

FROM node:14.18-alpine

RUN apk -U add openjdk8-jre git

# Install Docker client
RUN curl -fsSL https://download.docker.com/linux/static/stable/`uname -m`/docker-18.03.0-ce.tgz | tar --strip-components=1 -xz -C /usr/local/bin docker/docker

COPY --from=jnlp /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-agent
COPY --from=jnlp /usr/share/jenkins/agent.jar /usr/share/jenkins/agent.jar

ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
