FROM openjdk

EXPOSE 8000

WORKDIR /mydir 
COPY . .
WORKDIR /mydir/spring-example-project
RUN ./mvnw package
CMD java -jar ./target/docker-example-1.1.3.jar