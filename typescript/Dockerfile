FROM arm64v8/node:18.19.1-buster-slim

# Update local package index and run installs
RUN apt-get update

RUN apt-get install -y git sqlite

# Install global node modules for SAP CAP and frontend development
RUN npm install -g typescript vite

EXPOSE 8080
EXPOSE 8081
EXPOSE 5173