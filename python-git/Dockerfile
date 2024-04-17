FROM --platform=linux/arm64/v8 arm64v8/python:3.10.14

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates gnupg curl wget git && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install mkdocs mkdocs-material

RUN mkdir /home/projects
WORKDIR /home/projects