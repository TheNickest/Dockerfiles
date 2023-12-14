FROM --platform=linux/arm64 node:18.17-alpine

RUN apk update && apk upgrade
RUN apk add git
RUN addgroup -S yoyo && adduser -S yeoman -G yoyo

RUN npm install -g npm@latest

RUN npm install --global --silent yo generator-easy-ui5

ENV HOME /home/yeoman
ENV SHELL /bin/bash

USER yeoman
WORKDIR /home/yeoman

EXPOSE 3000
EXPOSE 8080