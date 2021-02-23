#	Docker learning Hub

###	Container: 
- a way to package application with all the necessary dependancies and configurations
- Portable artifact easily shared and moved around 
- Makes development and deployment more efficient

###	How containers improved the dev process
- before containers: installation process different on each OS environment
and many steps where something could go wrong
- After containers: own isolated environment packaged with all needed configuration
one command to install the app you can run same app with 2 different versions

###	How containers improved the deployment process
-Before containers: 
	- Configuration on the server needed
	- dependancy version conflicts
	- textual guide of deployment and this can lead to misunderstanding
- After containers:
	-Dev and operators work together to package the application in a container
	- No environmental config needed on server, except docker runtime

###	Technically speaking, a container is:
-Layer of images
- Mostly Lunix based Image, because small in size
- Application image on top

Docker images: its the actual package, an artifact that can be moved around 

Docker Vs Virtual Machine: they are both virtualization tools
-Docker virtualizes the application layer
 the size of docker images is much smaller
 Docker containers are much faster than the VM
 -Compatibility: VM of any OS can run on any OS HOST and we can't do that with docker
 That's why you have to check if the kernel is compatible with the Docker image if  not the Docker toolbox makes it possible.

 Some prerequisite Installation
 - Docker natively runs only on Windows 10 operating system

### Container vs Image
 - A container is a running environnment for images
 - Application image example : postgres, redis, mongoDB
 - Port binded: talk to application running inside of container
 - Virtual file system

##	Basic commands
docker ps : list running containers
docker run : starts new container with a command (pulls it and start if you don't have it)
docker ps -a : list running and running and stopped containers
docker start container_id
docker stop container_id

##	Container Port VS Host Port
We can have mutliple containers running in your host machine
Your laptop has only certain ports available
Conflict when same port on host machine

###	Ports binding specified in the docker run command
docker run -p6000:6367 redis: 6000 is the host port, 6367 is the container port, redis is the image running

###	TroubleShouting commands
you can rename you container names by adding "--name" on the docker run command

If one of your images have a problem you can see log: docker logs container-name or id

docker exec -it image_id: it means interactive terminal. this command is useful when you're running your own app in a container and check if everything is setup

##	Docker NETWORK
Container in the same docker network can talk to each other using just a container name without localhost port number etc. 
docker network create network_name

Docker compose: for running multiple Docker containers
Everything is set in a file.yaml in stead of creating a network and doing yourself each container run
NB: indentation in yaml is important

### start all the containers in the yaml
docker-compose -f file.yaml up -d

### to stop em all
docker-compose -f file.yaml down -d


There is no data persistance in the container itself

##	Dockerfile	 
blueprint for creating docker images
docker build -t myapp:1.0 .  *The dot at the end means the dockerfile is in the current directory*
PS: when you adjust a dockerfile, you MUST rebuilt the image

###	to delete a container
docker rm id_container

###	to delete an image
docker rmi id_image

##	Private Docker reposiotry with Amazon ECR
The service used is called Elastic Container Registry
- Create Docker Private repository
