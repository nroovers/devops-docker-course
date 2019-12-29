FROM ubuntu

RUN apt-get update
RUN apt-get install -y curl apt-transport-https ca-certificates gnupg-agent software-properties-common

RUN apt-get install -y git
RUN git config --global user.name "Nicolai Roovers"
RUN git config --global user.email "nroovers@gmail.com"

RUN curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt install -y nodejs

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) \ stable"
RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

EXPOSE 3000-3005