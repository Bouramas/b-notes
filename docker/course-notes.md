
## Docker Course Notes

These are my notes while watching the following course in Udemy:

https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/22776989#overview



Image: Single file with all the dependencies and configurations required to run a program (e.g. redis)
	- stored on your hard-drive

Container: Is a program with its on isolated set of hardware resources (memory, networking tech, hard-drive space)
 	- a process or a set of processes that has a grouping of resources specifically assigned to it


docker-cli (Docker Client): Tool that we use in order to interact with the Docker-Server or Docker Daemon
docker-deamon: Tool that is responsible for creating images, running containers, etc. 

docker-hub: a repository of free public images

image-cache: local storage of images



--------------

### Containers back-end

Namespacing: isolate resources per a process or a group of processes. name spacing is not only used for hardware, it can be also used for software elements as well. So, for example, we can namespace a process to:
 - restrict the area of a hard drive that is available 
 - restrict the network devices that are available
 - restrict the ability to talk to other processes 
 - restrict the ability to see other processes. 
These are all things that we can use namespace for to essentially limit the resources.

Control Groups (cgroups): A control group can be used to limit the amount of resources that a particular process can use. limit the amount of memory that a process can use, the amount of CPU,the amount of hard drive, input, input or input output, and the amount of network bandwidth as well.

So these two features put together can be used to really kind of isolate a single process and limit


All those are run in a Linux VM - created when installing docker for mac or windows

--------------

### Images back-end

Image is a File-System Snapshot - e.g. Chrome installation - So the snapshot is placed in a hard-drive slot that the container uses.
Image is a Startup Command - e.g. start Chrome - So the startup command is executed upon running the container.

--------------

	docker run IMAGE_NAME OVERIDE_COMMAND

	docker run = docker create + docker start
	Creating is about the FileSystem, starting it is about runnning/executing commands

	docker run hello-world
	or 
	docker create hello-word -> outputs CONTAINER_ID
	doker start -a CONTAINER_ID -> -a flag attaches to the container and prints the output in your terminal



	docker ps - list all running containers
	docker ps --all - list all containers that have ever been created on my machine
	docker system prune - Remove all stopped containers, networks, build cache


	docker logs CONTAINER_ID - get logs of a container

	docket stop CONTAINER_ID - a hardware signal (SIGTERM) is sent to the primary process of the container. 
	Provides some time to the container to perform a cleanup and gracefully stop

	docker kill CONTAINER_ID - issues a SIGKILL signal - shut down immediately

	docker exec -it CONTAINER_ID COMMAND_TO_EXECUTE

	the -it flag is actually 2 flags:
		-i > attach terminal to the 'standard in' (STDIN) channel of the running process
		-t > makes all text that shows up a little bit pretty 



	Docker RUN with PORT MAPPING
	docker run -p 8080:8080 IMAGE_ID
	-p 8080:8080 --> Route incoming requests to this port on local host to this port inside the container
	-p FROM(LOCALHOST):TO(CONTAINER)
	Note only incoming requests are limited, docker can reach out with outcoming requests


--------------

### DOCKERFILE

Specify a base image

Run some commands to install additional programs

Specify a command to run on container startup


NOTE: The order in which you put the instructions does make a difference. So make sure you're only copying the bare minimum for each successive step. In order not to trigger rebuilds for changing non-affecting files. I.e. first copy package.json which is used by RUN npm instal and then copy all the files containing your application's code.

--------------

### Docker Instructions

	FROM - which docker image to use as a base
	RUN  - execute some commands while we are preparing our custom image
	CMD - what to execute when the image is used to start a new container
	COPY - move files and folders from out local filesystem inside the container (COPY FROM(LOCAL) TO(CONTAINER))
	WORKDIR - specify the working directory inside the container - affects all commands in the Dockerfile and the CLI

### Docker Image Tagging
docker build -t dockerID/RepoName:Version .
the tag is used to refer to the image without needing to remember the ID

### Docker Cache
- Used to store already installed images
- If the order of installation changes - cache will not be used


Find images here:
hub.docker.com




------------- 

### Docker-Compose
- really exists to keep you from having to write repetitive commands with Docker CLI

	services:
		redis-server: 
			image: 'redis'
		node-app:
			restart: always
			build: .
			ports:
			 - 8081:8081
			 - Local:Container
		another-node-app:
			build:
				context: .
				dockerfile: Dockerfile.dev // specify dockerfile path
			ports:
			 - 8081:8081
			 - Local:Container

- In the first container we use the redis image
- In the second container we specify that the container should be built using the Dockerfile found in the current directory (.)
- service names - can be also used as host names in order to communicate with the services

	docker-compose up -> docker run Image
	docker-compose up -d -> -d start in the background
	docker-compose up --build -> docker build . + docker run Image
	docker-compose down -> stop and remove containers

Restart policies
- "no" - never attempt to restart this container if it stops or crashes (QUOTES REQUIRED since plain no in yaml means false)
- always - always attempt to restart it
- on-failure - only restart if the container stops with an error code
- unless-stopped - always restart unless we (the developers) forcibly stop it


---------------

### Docker Volumes
 - instead of copying a folder - reference it

in docker-compose:
		volumes:
			- /app/node_modules
			- .:/app
Here we specify that app/node_modules should be referenced from inside the container (do not try to override it) - and all other folder should be referenced from our local folder.


docker sbom - displays the SBOM (Software Bill Of Materials) of any Docker image. This feature outputs the SBOM in a table or can be exported into SPDX and CycloneDX formats.


### NGINX - Requests Router

NginX is watching for requests from the outside world and then routes them to the appropriate servers.
- Listens on a default port
- Redirects requests to 'upstream servers', example:
	+ if starts with /api/ --> go to a docker service we've exposed in /api:5000
	+ if starts with /view/ --> go to a docker service we've exposed in /react:3000
