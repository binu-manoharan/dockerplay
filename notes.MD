# Docker

## Set up

- present terminal with two tabs (squid/zeeton)
- get a mouse turn off touchpad if needed (search touchpad)
- set up macros
- clean up previous containers
```
alias stopcontainers='docker container stop `docker ps -aq`'
```
```
docker container rm `docker container ls -aq`
docker image rm hello-world
```


## Part 1

- Each instruction in Dockerfile creates a layer
- Union file system operate by creating layers making them lightweight and fast.
- UnionFS is used by docker as the building blocks for containers
- https://hub.docker.com/

## Part 2 - containers

```
docker run hello-world
docker image ls
docker container ls -a
cd hello-world-files
docker build . -t "my-hello-world"
```

- Mention why the container exits immediately
- Mention about scratch
- Show the layer created while building an image

## Part 3 - tomcat

create an index.html

```
FROM tomcat

RUN mkdir /usr/local/tomcat/webapps/test

COPY index.html /usr/local/tomcat/webapps/test

CMD catalina.sh run
```

- RUN executes commands in a new layer and creates new image (ex. install softwares)
- CMD sets default commands and parameters when docker container runs

- shell form executes command using sh -c
```
RUN echo "hi"
```
- exec form executes commands without any shell processing
```
RUN ["echo", "hi"]
```

## part 4 - tag and push image

```
docker login
docker tag my-tomcat binumanoharan/playground:my-tomcat
docker push binumanoharan/playground:my-tomcat
```

## part 5 - services

create an index.html

docker-compose.yml
```
version: '3'
services:
    tomcat:
        image: my-tomcat # work with the local copy
        ports:
            - 1234:8080
```

```
docker-compose up -d
docker inspect `docker ps -q` | grep "IPAddress"
```


## part 6 - stack

docker-compose.yml file
```
version: '3'
services:
    tomcat:
        image: my-tomcat
        ports:
            - 1234:8080
        # deploy:
        #   replicas: 5
        #   resources:
        #     limits:
        #       cpus: "0.1"
        #       memory: 50M
        #   restart_policy:
        #     condition: on-failure
        networks:
            - app-network
networks:
    app-network:

```

```
docker swarm init
docker stack deploy -c docker-compose.yml my-tomcat-stack
docker stack rm my-tomcat-stack
docker swarm leave --force
```

```
docker ps -q | xargs docker inspect | grep "IPAddress"
```
