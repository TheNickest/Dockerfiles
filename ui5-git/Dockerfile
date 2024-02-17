# base image
FROM --platform=linux/arm64/v8 node:20.10-buster-slim

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y git adduser

# Install global node modules
RUN npm install --global --silent npm@latest @ui5/cli yo typescript generator-easy-ui5

# Add Yeoman User
RUN adduser yeoman
RUN echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Yeoman needs the use of a home directory for caching and certain config storage.
ENV HOME /home/yeoman

RUN mkdir /ui5-projects && chown yeoman:yeoman /ui5-projects
WORKDIR /ui5-projects

# Always run as the yeoman user
USER yeoman

# Ports
EXPOSE 8080
EXPOSE 3000
EXPOSE 8000
EXPOSE 5173

CMD ["/bin/bash"]