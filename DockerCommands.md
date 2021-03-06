# Docker Commands

Get a list of all of the Docker commands:
```sh
docker -h
```

### Management Commands:

* ***builder*** Manage builds
* ***config*** Manage Docker configs
* ***container*** Manage containers
* ***engine*** Manage the docker engine
* ***image*** Manage images
* ***network*** Manage networks
* ***node*** Manage Swarm nodes
* ***plugin*** Manage plugins
* ***secret*** Manage Docker secrets
* ***service*** Manage services
* ***stack*** Manage Docker stacks
* ***swarm*** Manage Swarm
* ***system*** Manage Docker
* ***trust*** Manage trust on Docker images
* ***volume*** Manage volumes

### docker image:

* ***build*** Build an image from a dockerfile
* ***history*** Show the history of an image
* ***import*** Import the contents from a tarball to create a filesystem image
* ***inspect*** Display detailed information on one or more images
* ***load*** Load an image from a tar file or STDIN
* ***ls*** List images
* ***prune*** Remove unused images
* ***pull*** Pull an image or a repository from a registry
* ***push*** Push an image or a repository to a registry
* ***rm*** Remove one or more images
* ***save*** Save one or more images to a tar file (streamed to STDOUT by default)
* ***tag*** Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

### docker container:

* ***attach*** Attach local standard input, output, and error streams to a running container
* ***commit*** Create a new image from a container's changes
* ***cp*** Copy files/folders between a container and the local filesystem
* ***create*** Create a new container
* ***diff*** Inspect changes to files or directories on a container's filesystem
* ***exec*** Run a command in a running container
    + ***exec -it <container_id> /bin/bash*** enter/login into container terminal
* ***export*** Export a container's filesystem as a tar archive
* ***inspect*** Display detailed information on one or more containers
* ***kill*** Kill one or more running containers
* ***logs*** Fetch the logs of a container
* ***ls*** List containers
    + ***ls -a*** List containers inluding the ones that have been stopped
* ***pause*** Pause all processes within one or more containers
* ***port*** List port mappings or a specific mapping for the container
* ***prune*** Remove all stopped containers
* ***rename*** Rename a container
* ***restart*** Restart one or more containers
* ***rm*** Remove one or more containers
* ***run*** Run a command in a new container
    + ***run -P*** map all port existing for this container and mapped to a port random
* ***start*** Start one or more stopped containers
* ***stats*** Display a live stream of container(s) resource usage statistics
* ***stop*** Stop one or more running containers
* ***top*** Display the running processes of a container
* ***unpause*** Unpause all processes within one or more containers
* ***update*** Update configuration of one or more containers
* ***wait*** Block until one or more containers stop, then print their exit codes

# Creating Containers

### docker container run

* ***--help*** Print usage
* ***--rm*** Automatically remove the container when it exits
* ***-d, --detach*** Run container in background and print container ID
* ***-i, --interactive*** Keep STDIN open even if not attached
* ***--name string*** Assign a name to the container
* ***-p, --publish list*** Publish a container's port(s) to the host
* ***-t, --tty*** Allocate a pseudo-TTY
* ***-v, --volume list*** Mount a volume (the bind type of mount)
* ***--mount mount*** Attach a filesystem mount to the container
* ***--network string*** Connect a container to a network (default "default")

Create a container and attach to it:
```sh
docker container run –it busybox
```

Create a container and run it in the background:
```sh
docker container run –d nginx
```

Create a container that you name and run it in the background:
```sh
docker container run –d –name myContainer busybox
```

# Exposing and Publishing Container Ports

### Exposing
* Expose a port or a range of ports
* This does not publish the port
* Use `--expose [PORT]`
```sh
docker container run --expose 1234 [IMAGE]
```
### Publishing:
* Maps a container's port to a host`s port
* `-p` or `--publish` publishes a container's port(s) to the host
* `-P`, or `--publish-all` publishes all exposed ports to random ports
```sh
docker container run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]
docker container run -p [HOST_PORT]:[CONTAINER_PORT]/tcp -p [HOST_PORT]:[CONTAINER_PORT]/udp [IMAGE]
docker container run -P
```
ex: Here expose port 3000 of container but don't mapped. in another hand it mapped 8080 port from local host to port 80 of container. port 80 is exposed by default. So if you `curl localhost:8080` you will notice you have default page of nginx 
```sh
docker container run -d --expose 3000 -p 8080:80 nginx
```


### Lists all port mappings or a specific mapping for a container:
```sh
docker container port [Container_NAME]
```

# Executing Container Commands

Executing a command:
* Dockerfile
* During a Docker run
* Using the exec command

Commands can be:
* One and done Commands
* Long running Commands

### Start a container with a command:
```sh
docker container run [IMAGE] [CMD]
```
### Execute a command on a container:
```sh
docker container exec -it [NAME] [CMD]
```

Example:
```sh
docker container run -d -p 8080:80 nginx
docker container ps
docker container exec -it [NAME] /bin/bash
docker container exec -it [NAME] ls /usr/share/nginx/html/
```