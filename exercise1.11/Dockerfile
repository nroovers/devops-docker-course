FROM ubuntu

EXPOSE 8000

RUN apt-get update && apt-get install -y curl wget 
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

WORKDIR /mydir 
COPY . .
WORKDIR /mydir/backend-example-docker
RUN npm install webpack --save
CMD npm start