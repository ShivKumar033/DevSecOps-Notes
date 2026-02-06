- Docker is an open source platform that allows developers and systems administrators to package applications into containers.

### Auditing Tools
1. Docker-bench-security
	-  script that checks for dozens of common best-practices around deploying Docker containers in production.
	- [[https://github.com/docker/docker-bench-security]]

2. The Linux Auditing Framework
3. InSpec
4. Lynis

---
### Docker Images
- Is a static template that contains the application code, a runtime, system tools, libraries, and settings needed for an application to run consistently across different environments. 
- It is the blueprint from which Docker containers are created.

```c
# Build the docker images
docker build -t myapplication

# Remove the docker images 
docker rmi image_id
```


### Docker Container
- A Docker container is the live, running environment created from a Docker image. 
- It is a lightweight, isolated process that runs the application.

```c
# TO show Running Container
docker ps -a

# Run or start the container
docker run ngnix
docker start ngnix

# Delete the container 
docker rm container_id
docker rm -f $(docker ps -aq)

# Contianer port mapping 
docker run -d --name nginx  -p 8080:80 nginx

# Entract the container 
docker exec -it container_id bash
```