# Base build stage
FROM arm64v8/debian:latest as kraftkit

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates gnupg curl wget lsb-release && \
    rm -rf /var/lib/apt/lists/*

# kraftcloud kit
RUN wget https://github.com/unikraft/kraftkit/releases/download/v0.8.1/kraft_0.8.1_linux_arm64.tar.gz
RUN tar -xvf kraft_0.8.1_linux_arm64.tar.gz && \
    mv kraft /usr/local/bin/kraft && mv kraftld /usr/local/bin/kraftld && \
    chmod +x /usr/local/bin/kraft && chmod +x /usr/local/bin/kraftld

# Final build stage
FROM --platform=linux/arm64/v8 node:18.18.0-buster-slim

COPY --from=kraftkit /usr/local/bin/kraft /usr/local/bin/kraft
COPY --from=kraftkit /usr/local/bin/kraftld /usr/local/bin/krafld

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y sqlite3 git adduser
#RUN apt-get install -y git 

# Install global node modules for SAP CAP and frontend development
RUN npm install -g --silent @ui5/cli @sap/cds-dk yo npm@latest \
    generator-easy-ui5 @sap/generator-cap-project @sap/generator-fiori typescript

# Add a separate user than root to work with
RUN adduser yeoman
RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
ENV HOME /home/yeoman
ENV KRAFTCLOUD_TOKEN=cm9ib3QkbmJ1c2NoLnVzZXJzLmtyYWZ0Y2xvdWQ6RVRJeE15M2VSOVFjSVMxTEJ6MkFkaFJnRFV1U1BCTTM=
ENV KRAFTCLOUD_METRO=fra0
RUN mkdir /home/yeoman/projects && chown yeoman:yeoman /home/yeoman/projects

USER yeoman
WORKDIR /home/yeoman/projects

EXPOSE 4004
EXPOSE 5000
EXPOSE 5005
EXPOSE 8080