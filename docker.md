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

## Clean dangling/intermediate images

    docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

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

# Nvidia docker

## Install nvidia-docker

Follow instructions here: https://github.com/NVIDIA/nvidia-docker

## Test nvidia-docker

```
docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi
```

# Docker images

## Download docker image from gcr and peak inside

Use this if you have a docker image in GCR or other remote repo and want to peak inside without running it.

```
gcloud docker -- pull gcr.io/$PROJECT/$NAME:$TAG

# look for the image
docker image ls

# Get the image id from the IMAGE ID column
docker run --entrypoint "/bin/bash" -it $IMAGE_ID
```
