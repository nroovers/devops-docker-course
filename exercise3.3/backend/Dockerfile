FROM ubuntu:16.04

EXPOSE 8000

WORKDIR /app 
COPY ./backend-example-docker .

RUN apt-get update && \
    apt-get install -y curl wget && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt install -y nodejs && \
    npm install webpack --save && \ 
    apt-get purge -y --auto-remove curl && \ 
    rm -rf /var/lib/apt/lists/* && \
    useradd -m app && \
    chown app -R /app

USER app

CMD npm start