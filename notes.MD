# Docker

## Set up

- present terminal with two tabs (squid/zeeton)
- get a mouse turn off touchpad if needed (search touchpad)
- remove hello-world image

```
docker container rm `docker container ls -aq`
docker image rm hello-world
```


## Part 1

- Each instruction in Dockerfile creates a layer
- Union file system operate by creating layers making them lightweight and fast.
- UnionFS is used by docker as the building blocks for containers
- https://hub.docker.com/

## Part 2 - Hello world

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

## Part 3 - ubuntu

```
FROM ubuntu
CMD
```

- CMD and entrypoint
- shell and command mode for running commands 
