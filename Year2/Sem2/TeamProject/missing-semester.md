# Containers + Virtualisation
Containers started to be a thing in the mid 2000s - popular in mid 2010s
Good for managing complexity

Need to be able to be scaled up + down

These are technologies that take big computer into lots of small computers
Lets us change + upgrade parts individually

All containers are running linux, even on windows/macOS

### How are containers different to VMs
<span style="color:#00fc00">VM uses hardware</span> inside machine to create boundaries
How VMs work is interesting (google it)
Not much opportunity to share much

<span style="color:#00fc00">Containers uses abstractions to shield processes</span> from what they can see
Hiding host system and container from seeing each other
Can share resources between containers/host

Very lightweight - only need whats absolutely necessary

Containers based off on images
Can share images using registries
Bunch of free ones online - open source

Containers don't have a lot of things installed on them, have to install things yourself
## Using Docker
In Docker, images have tags
A layer is a part of the container
<span style="color:#00bfff">Containers are disposable</span>

Use `docker images` to show all images installed
Use `docker run -it <name> sh` to open a shell on an image. <span style="color:#00bfff">-it is magic</span> 

You can change stuff in the container without it affecting your host system

Use `docker ps` to show all containers currently running
`docker stop <container_id` to stop container
`docker kill <container_id` to kill container

### Storing data between runs
Done with volumes attached to containers
Volumes can be on network device
Create volumes with `docker create volume <name>`
List volumes with `docker volume ls`

Mount a volume to a container using `-v <volume_name>:/<directory>`
eg: `docker run -it -v foo:/home/foo ubuntu sh`

Should be able to connect one volume to multiple containers
Can connect volumes to preexisting directories on host system

Add container to network using `--network <network_name>`

#### Using images
create `Dockerfile`

In the Dockerfile:
```
FROM ubuntu

RUN apt-get update
RUN apt-get install -y iproute2 iputils-ping
```

Build image using `docker build -t <image_name> <directory>`

Reduce number of layers you have to decrease file size
Usually a single command creates a single layer
Can join together commands with `&&`

