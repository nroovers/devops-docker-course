FROM ubuntu:16.04
# FROM ubuntu:18.04

    # DEBIAN_FRONTEND="noninteractive" apt-get -y install tzdata && \
RUN apt-get update && \
    apt-get install -y rtmpdump wget ffmpeg python3-dev python3-setuptools \
      python3-pip python3-crypto python3-requests python3-lxml \
      php-cli php-curl php-xml php-bcmath && \
    pip3 install --user --upgrade yle-dl && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app 

ENTRYPOINT [ "/root/.local/bin/yle-dl" ]