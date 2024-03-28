FROM node:18-alpine
# Installing libvips-dev for sharp Compatibility
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev git
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}
### required additional env variables
ENV DATABASE_CLIENT=sqlite
ENV DATABASE_HOST=localhost
ENV DATABASE_PORT=3306
ENV DATABASE_NAME=strapi
ENV DATABASE_USERNAME=strapi
ENV DATABASE_PASSWORD=strapi
ENV JWT_SECRET=u/nE/dyUsQ3HwwaE8rrunA==
ENV ADMIN_JWT_SECRET=s9YK2qNEpoclUI+OBbcqFQ==
ENV APP_KEYS=g4A3TzFUZ5iWdkh1paQsGQ==,L4dn/fnDOY0gofbSwFCGGg==,0GQZIIfqOhmHTICyF1eFHQ==,7V/vMSPshMZDjNm2+7nKiQ==
###

WORKDIR /opt/
COPY package.json package-lock.json ./
RUN npm install -g node-gyp
RUN npm config set fetch-retry-maxtimeout 600000 -g && npm install
ENV PATH /opt/node_modules/.bin:$PATH

WORKDIR /opt/app
COPY . .
RUN chown -R node:node /opt/app
USER node
RUN ["npm", "run", "build"]
EXPOSE 1337
CMD ["npm", "run", "develop"]
