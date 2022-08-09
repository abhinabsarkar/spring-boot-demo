# Docker hub image - abhinabsarkar/spring-boot-session-azure-redis:v1.1.0

A sample docker app built on Alpine linux running java version 8 running Spring Boot application. The sample application is making use of HttpSession to achieve Session management using Azure Cache for Redis. 

Refer the [dockerfile](/code/dockerfile) which has steps to create multi-stage build using the jdk image & then a runtime image.

The docker image can be downloaded from docker hub by running the below command 
```bash
docker pull abhinabsarkar/spring-boot-session-azure-redis:v1.1.0
```

### To build the image, run docker build from the root directory of the application
```bash
# Build the abs image
docker build -t spring-boot-session-azure-redis:v1.1.0 .
# Run the docker container locally
docker run --name abs-test-container -d -p 8080:8080 spring-boot-session-azure-redis:v1.1.0
# Check the status of the container
docker ps -a | grep abs-test-container
# Test the app
curl http://localhost:8080
# log into the running container. The runtime image doesn't have bash
docker exec -it abs-test-container /bin/sh
docker exec -it abs-test-container <command>
# Push the image to docker hub
docker login
# Tag the local image & map it to the docker repo
docker tag local-image:tagname new-repo:tagname
# eg: docker tag spring-boot-session-azure-redis:v1.1.0 abhinabsarkar/spring-boot-session-azure-redis:v1.1.0
# push the tagged image to the docker hub
docker push new-repo:tagname
# eg: docker push abhinabsarkar/spring-boot-session-azure-redis:v1.1.0

# Remove the container
docker rm abs-test-container -f
# Remove the image
docker rmi spring-boot-session-azure-redis:v1.1.0
```