FROM ubuntu

RUN apt-get update && apt-get install -y curl wget 
COPY start.sh . 
RUN chmod +x ./start.sh

CMD ["./start.sh"]