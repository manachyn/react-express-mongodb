FROM node:lts-buster-slim AS development

WORKDIR /usr/src/app

COPY backend/package.json ./
COPY backend/package-lock.json ./

RUN npm ci

COPY backend/ .

EXPOSE 3000

CMD [ "npm", "start" ]

FROM development as production

RUN npm ci --only=production

COPY --from=development /usr/src/app .

CMD [ "npm", "start" ]