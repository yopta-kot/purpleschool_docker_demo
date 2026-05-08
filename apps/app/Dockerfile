FROM node:15-alpine AS node

WORKDIR /app/apps/app
COPY ./apps/app/package*.json ./
RUN npm ci

COPY . ../../
WORKDIR /app
RUN npm ci

WORKDIR /app/apps/app
RUN PUBLIC_URL=http://127.0.0.1:3001 npm run build

FROM nginx:1.13

COPY --from=node /app/apps/app/build /usr/share/nginx/html
COPY ./apps/app/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80