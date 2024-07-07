# base image
FROM --platform=linux/arm64/v8 node:20.15-buster-slim

# Update local package index and run installs
RUN apt-get update && apt-get upgrade

RUN apt-get install -y git adduser

# Install global node modules
RUN npm install -g --silent npm@latest \
    yo typescript @sap/generator-cap-project @sap/cds-dk

# Add Yeoman User
RUN adduser yeoman
RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Yeoman needs the use of a home directory for caching and certain config storage.
ENV HOME /home/yeoman

RUN mkdir /projects && chown yeoman:yeoman /projects

# Always run as the yeoman user
USER yeoman
WORKDIR /projects

# Ports
EXPOSE 8080
EXPOSE 3000
EXPOSE 4004
EXPOSE 8000
EXPOSE 5173

CMD ["/bin/bash"]