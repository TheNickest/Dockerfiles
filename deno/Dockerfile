FROM --platform=linux/arm64 denoland/deno:ubuntu-1.41.3

RUN apt-get update -y
RUN apt-get install -y git

RUN mkdir /home/deno && chown deno:deno /home/deno

USER deno
WORKDIR /home/deno

EXPOSE 8080
EXPOSE 8081