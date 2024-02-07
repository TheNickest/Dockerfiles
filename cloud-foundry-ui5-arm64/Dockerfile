# Base build stage
FROM arm64v8/debian:latest as foundry

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates gnupg curl wget && \
    rm -rf /var/lib/apt/lists/*

# Install the Cloud Foundry CLI
RUN curl -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=v8" | tar -zx && \
    mv cf8 /usr/local/bin/cf && \
    chmod +x /usr/local/bin/cf

RUN wget https://github.com/SAP/cloud-mta-build-tool/releases/download/v1.2.27/cloud-mta-build-tool_1.2.27_Linux_arm64.tar.gz
RUN tar -xvzf cloud-mta-build-tool_1.2.27_Linux_arm64.tar.gz && \
    mv mbt /usr/local/bin/mbt && \
    chmod +x /usr/local/bin/mbt

# Final build stage
FROM arm64v8/node:20.11.0-buster-slim

COPY --from=foundry /usr/local/bin/cf /usr/local/bin/cf
COPY --from=foundry /usr/local/bin/mbt /usr/local/bin/mbt

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y sqlite3 git adduser
#RUN apt-get install -y git 

# Install global node modules for SAP CAP and frontend development: mbt
RUN npm install -g --silent @ui5/cli @sap/cds-dk yo npm@latest \
    generator-easy-ui5 @sap/generator-cap-project @sap/generator-fiori

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