# syntax=docker/dockerfile:1.4

FROM node:lts-buster-slim AS development

# Create app directory
WORKDIR /usr/src/app

# Copying package.json and package-lock.json
COPY backend/package*.json ./

# Install app dependencies
RUN npm ci --only=production

# Bundle app source
COPY backend/ .

EXPOSE 3000

CMD [ "npm", "start" ]