# Docker cheat sheet

## Administration

**Docker file optimization**  
https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/  
https://docs.microsoft.com/en-us/virtualization/windowscontainers/manage-docker/optimize-windows-dockerfile  

**Troubleshooting**  
https://docs.docker.com/docker-for-windows/troubleshoot/  

**Kitematic: ENOENT error**  
In case of this certification error on Windows:  
`ENOENT: no such file or directory, open '/Users/<user>/.docker/machine/machines/default/ca.pem'`  
It can be fixed by running the following command:  
`docker-machine -D regenerate-certs default`  


## Commands

**Show version/info**  
`docker version`  
`docker --version`  
`docker info`  

**List containers** (by default only *running* status)  
Arguments:  
`-a` All.  
`-s` Size.  

`docker ps -as` The list of containers shows some network configuration. If **Ports** shows 0.0.0.0, it means that is listening on **localhost**.

**List images**  
`docker images`

**List machines**  
`docker-machine ls`

**Download image from repository**  
By default, it will try to get *latest* tag.  
Syntax: `docker pull <username>/<image>:<tag>`  
`docker pull microsoft/windowsservercore`  
`docker pull centos:latest`  

**Create image from container**  
Arguments:  
`-a --author`  
`-m --message`  

Syntax: `docker commit <container> <image>:<tag>`  
`docker commit -a <author> -m "Added coreutils" alpine <username>/alpine:latest`  
`docker image inspect a12ed74ff7ee` Display detailed information on one or more images.  

**Create image from Dockerfile**  
Arguments:  
`-t` Tag.  
`.` Indicates the context, where the Dockerfile is located.  

`docker build -t friendlyhello .`

**Create/Execute container**  
By default, it will try to get *latest* tag.  
Arguments:  
`-e --env` Set environment variables.  
`-t --tty` Allocate a pseudo-TTY.  
`-i --interactive` Keep STDIN open even if not attached.  
`-d --detach` Detached (run in background).  
`-p <hostPort>:<containerPort>` Publish or expose port.  

`docker create --name <name> -it <image>` Creates the container without starting it.  
`docker run` Creates the container and starts it.  
`docker run -p 4000:80 <username>/<repository>:<tag>` Maps port 4000 to 80.  
`docker run -d -p 9000:9000 --name portainer portainer/portainer`

**Start/Stop container**   
It can be used both ID or name of the container.  
`docker stop <container>`  
`docker start <container>`  

**Delete containers**  
`docker rm -f <container>`  
`docker rm -f (docker ps -aq)` Deletes all of them.  

**Create machine**  
`docker-machine create test`  

**Start/Stop machine**  
`docker-machine stop default`  
`docker-machine start default`

**Show steps/layers image history**  
`docker history <image>`

**Show running processes in container**  
`docker top <container>`

**Delete images**  
`docker rmi <image>`  
`docker images rm <image>`  
`docker rmi -f (docker images -q)` Deletes all of them.

**Login to Docker account**  
`docker login`

**Tag image to upload**  
Syntax: `docker tag <image> <username>/<repository>:<tag>`  
`docker tag 0c516569f0b6 <username>/alpine:v1`  
`docker tag a12ed74ff7ee <username>/alpine:latest`

**Upload image to Docker Hub**  
Syntax: `docker push <image>:<tag>`  
`docker push <username>/python:test`  
`docker push <username>/alpine:latest`

**Search in Docker Hub**  
`docker search alpi*`

**Container networking**  
`docker network ls` List networks  
`docker port <container>` Shows port configuration.  
`docker network connect <network> <container>`  
`docker network disconnect <network> <container>`


## Docker Hub
https://hub.docker.com/

**Linux**  
Minimal Docker image based on Alpine Linux.  
https://hub.docker.com/_/alpine/

**BBDD**  
https://hub.docker.com/_/mysql/  
https://hub.docker.com/r/mysql/mysql-server/  
https://hub.docker.com/_/oracle-database-enterprise-edition  

**Big Data**  
https://hub.docker.com/_/mongo  
https://hub.docker.com/_/cloudera-quickstart  
https://hub.docker.com/_/couchbase

**Docker GUI**  
https://hub.docker.com/_/coscale-agent  
https://hub.docker.com/r/portainer/portainer/  
https://hub.docker.com/_/datadog-agent  
