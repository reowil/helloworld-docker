# Helloworld-Docker

Just playing around, trying stuff out.

Guide: [https://spring.io/guides/gs/spring-boot-docker/](https://spring.io/guides/gs/spring-boot-docker/)

## Running app as standalone app 
- Package it: `mvn package`
- Run the packaged app: `java -jar target/helloworld-docker-1.0-SNAPSHOT.jar` (using the right file name, depending on the version)
- Or combine the two: `mvn package && java -jar target/helloworld-docker-1.0-SNAPSHOT.jar`

## Using Spotify dockerfile-maven-plugin 
### Building Docker image 
`mvn install dockerfile:build` 

*Note:* For this to work (using the Spotify plugin on Windows), Daemon on tcp://localhost:2375 has to be exposed without TLS. Which is not a good idea. (This is done in the Docker Settings.) *Remember to stop exposing the daemon without TLS when you're done playing.* 

### Pushing Docker image 
`mvn dockerfile:push` 

Note: `pom.xml` contains an execution element which (if not commented out...) automatically runs dockerfile:push when you do mvn install. 

## Using Docker

### Building Docker image ("by hand", not using Maven and the Spotify plugin)
`docker build -t halla --build-arg JAR_FILE=target/helloworld-docker-1.0-SNAPSHOT.jar` (using the right file name)

### Running app in Docker container
`docker run -p 8080:8080 -t hellodocker/helloworld-docker` 

Include a `-d` to run in detached mode (i.e. in the background). 

### See running containers 
`docker ps` 

### Stop the container 
`docker container stop <name/container_id>`

### Handling Docker images
- List installed images: `docker image ls`
- Remove image: `docker image rm <name>`