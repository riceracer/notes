# Docker

## copy file from container to host

    docker cp <CONTAINER>:/container/file/path /host/file/path
    
## Cleanup containers

```
docker container ls -a
docker container rm CONTAINER_IR
```

## Prune unused images

Remove local images that are no longer associated with a container

    docker image prune

# Docker-compose

## run a container 

Don't start the default entrypoint or if it has no entrypoint:

```
# specific
docker-compose -f compose-build.yml run container_name bash

# generic
docker-compose -f compose-build.yml run CONTAINER_NAME COMMAND
```

If you need to override entrypoint - the --entrypoint option must be BEFORE the container name

```
docker-compose -f docker-compose.yml run --entrypoint bash container_name

# generic 
docker-compose run --entrypoint COMMAND CONTAINER_NAME
```

* https://docs.docker.com/compose/reference/run/
