FROM ubuntu:latest

ARG PORT=12345

RUN apt-get update
RUN apt-get install -y curl && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN apt-get install -y lsb-release software-properties-common apt-transport-https
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get update && apt-cache policy docker-ce
RUN apt-get install -y docker-ce
RUN mkdir /etc/docker
EXPOSE $PORT
