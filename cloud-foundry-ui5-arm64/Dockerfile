# Base build stage
FROM arm64v8/debian:latest as foundry

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates gnupg curl && \
    rm -rf /var/lib/apt/lists/*

# Install the Cloud Foundry CLI
RUN curl -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=v8" | tar -zx && \
    mv cf7 /usr/local/bin/cf && \
    chmod +x /usr/local/bin/cf

# Final build stage
FROM arm64v8/node:20-buster-slim

COPY --from=foundry /usr/local/bin/cf /usr/local/bin/cf

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y sqlite3 git adduser
#RUN apt-get install -y git 

# Install global node modules for SAP CAP and frontend development: mbt
RUN npm install -g --silent @ui5/cli @sap/cds-dk yo npm@latest

# Add a separate user than root to work with
RUN adduser yeoman
RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
ENV HOME /home/yeoman
RUN mkdir /projects && chown yeoman:yeoman /projects

USER yeoman
WORKDIR /projects

EXPOSE 4004
EXPOSE 5000
EXPOSE 8080
EXPOSE 8081