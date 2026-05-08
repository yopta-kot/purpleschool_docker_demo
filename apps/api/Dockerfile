# FROM node:15-alpine as build
# WORKDIR /opt/app
# ADD *.json ./
# RUN npm ci
# ADD . .
# RUN npm run build api
# CMD [ "node", "./dist/apps/api/main.js" ]

FROM node:15-alpine as build
WORKDIR /opt/app
ADD *.json ./
RUN npm ci
ADD . .
RUN npm run build api

FROM node:15-alpine
WORKDIR /opt/app
ADD *.json ./
RUN npm ci --omit=dev
COPY --from=build /opt/app/dist/apps/api ./dist

CMD [ "node", "./dist/main.js" ]