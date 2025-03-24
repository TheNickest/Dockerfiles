FROM node:22.4-slim

RUN apt-get update && \
    apt-get upgrade && \
    apt-get install -q -y git adduser

RUN npm install -g --silent typescript ts-node @sap/cds-dk yo \
    @sap/generator-cap-project

RUN adduser yeoman
RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
ENV HOME /home/yeoman
RUN mkdir /home/yeoman/projects && chown yeoman:yeoman /home/yeoman/projects

USER yeoman
WORKDIR /home/yeoman/projects

EXPOSE 4004
EXPOSE 5000
EXPOSE 5005
EXPOSE 8080