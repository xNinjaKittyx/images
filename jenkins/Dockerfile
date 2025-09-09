FROM jenkins/inbound-agent:latest-alpine-jdk11

USER root
RUN apk add --update --no-cache rsync curl

RUN curl -Lo gotify https://github.com/gotify/cli/releases/download/v2.3.2/gotify-cli-linux-amd64 && \
  chmod +x gotify && mv gotify /usr/bin/gotify && gotify version

USER jenkins
