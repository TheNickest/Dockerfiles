FROM ubuntu:20.04 as downloader

ARG TARGETPLATFORM
ARG VERSION

SHELL ["/bin/bash", "-c"]

RUN apt-get update -y
RUN apt-get install -y unzip curl

RUN [ "$TARGETPLATFORM" == "linux/arm64" ] && curl -Lsf https://github.com/LukeChannings/deno-arm64/releases/download/${VERSION}/deno-$(echo $TARGETPLATFORM | tr '/' '-').zip -o deno.zip || true
#RUN [ "$TARGETPLATFORM" == "linux/amd64" ] && curl -Lsf https://github.com/denoland/deno/releases/download/${VERSION}/deno-x86_64-unknown-linux-gnu.zip -o deno.zip || true

RUN unzip deno.zip && rm deno.zip

FROM ubuntu:20.04 as deno

COPY --from=downloader /deno /bin/deno
RUN chmod 755 /bin/deno

RUN addgroup --gid 1993 deno
RUN adduser --uid 1993 --gid 1993 deno
RUN mkdir /deno-dir/
RUN chown deno:deno /deno-dir/

ENV DENO_DIR /deno-dir/
ENV DENO_INSTALL_ROOT /usr/local

#FROM ubuntu:20.04

ARG TOKEN 
ARG USERNAME
ARG REPO

RUN apt-get update -y
RUN apt-get install -y git
WORKDIR /
RUN git clone https://${TOKEN}@github.com/${USERNAME}/${REPO}.git

EXPOSE 8080