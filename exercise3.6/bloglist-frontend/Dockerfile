FROM node AS build-stage

WORKDIR /app
COPY ./frontend .

RUN npm install && \
    npm run build

FROM nginx

COPY --from=build-stage /app/build/ /usr/share/nginx/html

EXPOSE 80