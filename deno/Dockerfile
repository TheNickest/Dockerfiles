FROM --platform=linux/arm64 denoland/deno:ubuntu-1.41.3

RUN apt-get update -y
RUN apt-get install -y git

RUN mkdir /projects && chown deno:deno /projects

USER deno
WORKDIR /projects

EXPOSE 8080
EXPOSE 8081