FROM node:15-alpine AS build
WORKDIR /opt/app
ADD *.json ./
RUN npm ci
ADD . .
RUN npm run build converter

FROM node:15-alpine
WORKDIR /opt/app
ADD *.json ./
RUN npm ci --omit=dev
COPY --from=build /opt/app/dist/apps/converter ./dist
CMD ["node", "./dist/main.js"]