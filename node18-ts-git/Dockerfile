FROM --platform=linux/arm64 node:18.17-alpine

RUN apk update && apk upgrade
RUN apk add git
RUN addgroup -S yoyo && adduser -S yeoman -G yoyo

RUN npm install -g npm@latest

RUN npm install --global --silent yo generator-easy-ui5 typescript mocha @ui5/cli

#RUN adduser -D yeoman
#RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV HOME /home/yeoman
ENV SHELL /bin/bash

RUN mkdir /ui5-projects && chown yeoman:yeoman /ui5-projects
WORKDIR /ui5-projects

USER yeoman

EXPOSE 3000
EXPOSE 8080