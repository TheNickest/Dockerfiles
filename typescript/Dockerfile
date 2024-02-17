FROM arm64v8/node:18-buster-slim

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y git

# Install global node modules for SAP CAP and frontend development
RUN npm install -g typescript

EXPOSE 8080
EXPOSE 8081