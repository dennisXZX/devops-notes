## Docker

#### Fundamentals

<img src="./images/docker.jpg" width="640" height="380" alt="docker vs hypervisor">

Docker creates a virtual machine and installs a Linux system on it behind the scene, so all the future containers will be run on this settings.

Once you have docker installed on your machine, run `docker version` to check the docker client and docker server info. Then run `docker run hello-world` to see if docker works properly. Docker client would tell docker server to spin up a new container (an instance of hello-world image), the latter would first check the image cache in your local machine to see if you already have the above-mentioned image. The docker server would reach out the docker hub to grab the image if you don't have one ready to serve.

`docker create image_name` create an instance of the image

`docker start container_id` run the startup command of the instance

`docker run image_name` is equal to `docker create` + `docker start`

`docker ps` list all running containers 

`docker ps --all` list all created containers

`docker stop container_id` tell a running container to shut itself down

`docker kill container_id` kill a running container right away

`docker system prune` remove all stopped containers, dangling images and build cache

`docker logs container_id` show all the logs emitted by a container

`docker exec -it container_id sh` get into the shell of the container

`docker exec -it container_id command` to run a command inside a container

For example, you can run `redis-cli` in a Redis container by `docker exec -it 093b6e72ff2b redis-cli`

The `-i` flag allows us to provide input from terminal to standard input of the running process in the container

#### Create a docker image

1. Create a Dockerfile

Create a file called `Dockerfile` in your docker image folder, no file extension is needed.

```
# use an existing docker image as a base
FROM alpine

# download and install dependencies
RUN apk add --update redis

# set up startup commands
CMD ["redis-server"]
```

2. Build and tag the image by running `docker build -t docker_id/project_name:latest .` in the docker image folder.

#### Build a Node.js app using Docker

Create a `Dockerfile` as follows:

```
# use an existing docker image as a base
FROM node:alpine

# copy everything from local machine to the container
# first argument is path relative to build context
# second argument is path inside the container
COPY ./ ./
# download and install dependencies
RUN npm install

# set up startup commands
CMD ["npm start"]
```

When the docker image is successfully built, run `docker run -p 5000:8080 image_name`.

The `-p 8080:8080` flag maps the incoming requests to localhost to the port inside the container.
