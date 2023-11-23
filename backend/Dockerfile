# syntax=docker/dockerfile:1.4

FROM node:lts-buster-slim AS development

# Create app directory
WORKDIR /usr/src/app

# Copying package.json and package-lock.json from the correct directory
COPY backend/package.json backend/package-lock.json /usr/src/app/

# Install app dependencies
RUN npm ci

# Copying the rest of the application from the correct directory
COPY backend/ /usr/src/app/

EXPOSE 3000

CMD [ "npm", "run", "dev" ]

FROM development as dev-envs
# Fixing the syntax for the RUN command
RUN apt-get update && apt-get install -y --no-install-recommends git

# Adding user vscode and group docker
RUN useradd -s /bin/bash -m vscode && groupadd docker && usermod -aG docker vscode

# Install Docker tools (cli, buildx, compose)
# The COPY command is commented out as the source image gloursdocker/docker is not specified in the Dockerfile
# COPY --from=gloursdocker/docker / /
CMD [ "npm", "run", "dev" ]