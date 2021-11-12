# Docker Commands

## Building and Deploying Images
### List images
`docker images`
### Build an image 
`docker build -t service-name:tag .`
- Must have a Dockerfile in current directory.
## Run a container
`docker run -d -p 80:80 docker/getting-started`
### List Running Containers
`docker container ls`
### List Containers including stopped ones
`docker container ls -a`
### Check logs
`docker container logs CONTAINER_ID`
### Stop Container
`docker container stop CONTAINER_ID`
### Remove Container
`docker container rm CONTAINER_ID`
### Remove Image forcibly
`docker rmi -f IMAGE_TAGE_ID`

---
## Removing Containers

### Remove all unused objects
`docker system prune`

`docker system prune --volumes`

### Remove all stopped containers

`docker container ls -a --filter status=exited --filter status=created`

OR

`docker container prune`

### That were created 12h ago
`docker container prune --filter "until=12h"`

### Stop and remove all
`docker container stop $(docker container ls -aq)`

`docker container rm $(docker container ls -aq)`

---
## Removing Images 

### All images
`docker image prune`

### Remove selective image
`docker image rm IMAGE_ID`

#### Which are not referenced by any existing container
`docker image prune -a`

### Using filter
`docker image prune -a --filter "until=12h"`

---
## Removing volumes

`docker volume ls`

`docker volume prune`

---
## Network
### Create a Network
`docker network create myNetwork`
### List all Networks
`docker network list`
### Run Redis in Network
`docker run --name redis.networked -d -p 6379:6379 --network myNetwork redis`
### Inspect Network
`docker network inspect myNetwork`
### Run your app in same network
`docker run --name node.networked -d -p 3001:3001 -e REDIS_URL=redis://redis.networked:6379 --network myNetwork myapp:latest`

---
## Removing Networks
### List all networks
`docker network ls`
### Remove selective network
`docker network rm NETWORK_ID`
### Remove all networks
`docker network prune`
### Rhat were created 12h ago
`docker network prune -a --filter "until=12h"`

[Reference](https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/)