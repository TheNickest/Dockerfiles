FROM arm64v8/node:20-buster-slim

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y git 

# Install global node modules for SAP CAP and frontend development
RUN npm install -g @angular/cli

EXPOSE 4200
EXPOSE 9876