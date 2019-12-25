FROM ubuntu

EXPOSE 5000

RUN apt-get update && apt-get install -y curl wget 
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

WORKDIR /mydir 
COPY . .
WORKDIR /mydir/frontend-example-docker
RUN npm install webpack --save
ENV API_URL=http://localhost:3005/
CMD npm start