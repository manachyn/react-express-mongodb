# syntax=docker/dockerfile:1.4

FROM node:lts-buster-slim AS development

# Create app directory
WORKDIR /usr/src/app

# Copying package.json and package-lock.json
COPY ./backend/package.json ./backend/package-lock.json ./

# Install app dependencies
RUN npm ci

# Bundle app source
COPY ./backend/ .

EXPOSE 3000

CMD [ "npm", "run", "dev" ]

FROM development as dev-envs
RUN apt-get update && apt-get install -y --no-install-recommends git

RUN useradd -s /bin/bash -m vscode && groupadd docker && usermod -aG docker vscode

# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /
CMD [ "npm", "run", "dev" ]