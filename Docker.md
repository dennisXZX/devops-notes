## Docker

#### Fundamentals

[CNCF Cloud Native Interactive Landscape](https://landscape.cncf.io/format=landscape)

<img src="./images/docker.jpg" width="640" height="380" alt="docker vs hypervisor">

For Mac/Windows, Docker creates a virtual machine and installs a Linux system on it behind the scene, so all the future containers will be running on this settings. You would need to connect to the Docker VM itself first to see the running processes (`ps aux`).

Once you have docker installed on your machine, run `docker version / docker info` to check the docker info, or `docker` to find out all the possible commands. Then run `docker run hello-world` to see if docker works properly. Docker client would tell docker server to spin up a new container (an instance of 'hello-world' image), the latter would first check the image cache in your local machine to see if you already have the above-mentioned image. The docker server would reach out the docker hub to grab the image if you don't have one ready to serve.

#### Container

`docker container COMMAND --help` gets all the options for a particular command

`docker container run --publish 8080:80 --name webhost --network my_app_net --env NGINX_ROOT_PASSWORD=yes nginx:latest` to spin up a container off the 'nginx' image and assign it to my_app_net private network

Here is what really happens behind the sciene:

1. Looks for the 'nginx' image locally in image cache first
2. Looks in remote image repository if the image cannot be found locally, downloads the latest version of 'nginx:latest' from Docker Hub
3. Create a new container from that image and prepares to start
4. Gives the container a virtual IP on a private network inside docker engine
5. Opens up port 8080 on the host and forwards to port 80 in the container
6. Starts the container by using commands specified in the image `Dockerfile`

`docker container run CONTAINER_NAME` always starts a new container from the image you specify. `--detach | -d` runs the container in the background, `--name CONTAINER_NAME` assigns a name to the container, `--env` adds environment variable, `-it` starts new container interactively

`docker container run -it --name proxy nginx bash`, starts a 'nginx' container with a bash command

`docker container exec -it CONTAINER_NAME COMMANDS`, runs additonal commands in a running container

`docker container start CONTAINER_NAME` starts an existing stopped container, `-ai` flag to get into the container standard input

`docker container stop CONTAINER_NAME` stops a running container

`docker container stop / rm $(docker container ls -aq)` to stop / remove all running containers

`docker container ls` lists all the running containers, `-a` flag to list all created containers

`docker container logs CONTAINER_NAME` shows logs for a container, `-f` flag to follow log output

`docker container rm CONTAINER_NAME` removes a container, add `-f` flag to remove a running container

`docker container top CONTAINER_NAME` lists running processes in a specific container

`docker container inspect CONTAINER_NAME` shows meta data about a container

`docker container stats` shows live performance data for all containers

#### Network

`docker network ls` lists all the private networks

`docker network inspect NETWORK_NAME` inspects a private network

`docker network create NETWORK_NAME` creates a private network

`docker network connect NETWORK_NAME CONTAINER_NAME` assigns the container to a new private network

#### Image

`docker search IMAGE_NAME` search docker image on docker hub

`docker pull IMAGE_NAME` pull the docker image from docker hub

`docker image ls` list all the docker images on your machine

`docker create IMAGE_NAME` create an instance of the image

`docker start CONTAINER_NAME` run the startup command of the instance, use `-ai` flag to attach the STDOUT/STDERR

`docker run -d IMAGE_NAME` is equal to `docker create` + `docker start`. Use `-d` flag to run containers in the background

`docker ps` list all running containers 

`docker ps --all` list all created containers

`docker stop CONTAINER_NAME` tell a running container to shut itself down (give the process a chance to do some clean up work)

`docker image rm CONTAINER_NAME` to remove an image

`docker kill CONTAINER_NAME` kill a running container right away

`docker system prune` remove all stopped containers, dangling images and build cache

`docker logs CONTAINER_NAME` show all the logs emitted by a container

`docker exec -it CONTAINER_NAME sh` get into the shell of the container, you can exit the container by using `Ctrl P + Q` but keep the container running. Typing `exit` inside the container would also stop the container.

`docker exec -it CONTAINER_NAME command` to run a command inside a container

For example, you can run `redis-cli` in a Redis container by `docker exec -it 093b6e72ff2b redis-cli`

The `-i` flag allows us to provide input from terminal to standard input of the running process in the container

#### Build

`docker build -t=IMAGE_NAME:v1.0.0 .` build an image using what's in the current folder

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

#### Build a simple Node.js app

Create a `Dockerfile` as follows:

```
# use an existing docker image as a base
FROM node:alpine

# set the working directory, any following command will be executed relative this path
WORKDIR /usr/app

# copy the package.json from local machine to the container
# so that even you change your code NPM will not re-install all your packages
# first argument is path relative to build context
# second argument is path inside the container
COPY ./package.json ./
# download and install dependencies
RUN npm install

# copy everything from local machine to the container
COPY ./ ./

# set up startup commands
CMD ["npm", "start"]
```

Run `docker build -t dennisxiao/simpleweb .` to build the docker image.

When the docker image is successfully built, run `docker run -p 5000:8080 image_name`.

The `-p 8080:8080` flag maps the incoming requests to localhost to the port inside the container.

#### Build a visitor counter app

Architecture: One Redis docker is used to store the visitor count, while you can scale up the Node.js docker to handle more traffic.

```
Node.js Docker ---> |------------|
Node.js Docker ---> |Redis Docker|
Node.js Docker ---> |____________|
```

1. Create a `Dockerfile` with the same setting as the simple Node.js app

2. Run `docker build -t dennisxiao/visit .` to build the docker image

3. In order for the Node.js container to communicate with the Redis docker, we need to use `docker-compose`. Create a `docker-compose.yml` file with the following content.

```
version: '3'

services: 
  redis-server:
    image: 'redis'
  node-app:
    restart: always
    build: .
    ports:
      - "8080:8080"
```

Then you can use `docker-compose up` to launch all containers, or `docker-compose up --build` to build the image and launch all containers.

#### Docker compose

`docker-compose up -d` run all the containers in the background

`docker-compose down` shut down all the containers

`docker-compose ps` list all the running containers
