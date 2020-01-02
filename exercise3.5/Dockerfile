FROM node:alpine as build-stage

WORKDIR /app
COPY ./frontend-example-docker .

RUN npm install webpack --save && \
    npm run build 

FROM nginx

COPY --from=build-stage /app/dist/ /usr/share/nginx/html

EXPOSE 80