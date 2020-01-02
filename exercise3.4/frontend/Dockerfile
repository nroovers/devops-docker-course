FROM node:alpine

EXPOSE 5000

WORKDIR /app
COPY ./frontend-example-docker .

    # apt-get update && \
    # apt-get install -y curl wget && \
    # curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    # apt install -y nodejs && \
    # npm install webpack --save && \ 
    # apt-get purge -y --auto-remove curl && \ 
    # rm -rf /var/lib/apt/lists/* && \

RUN npm install webpack --save && \ 
    adduser -D app && \
    chown -R app /app

USER app

CMD npm start