FROM node:alpine

EXPOSE 8000

WORKDIR /app 
COPY ./backend-example-docker .

RUN npm install webpack --save && \ 
    adduser -D app && \
    chown -R app /app

USER app

CMD npm start