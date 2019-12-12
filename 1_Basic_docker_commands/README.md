## BASIC DOCKER COMMANDS 
> Fedora Terminal Based Commands 

### To check the docker version on the system
 
```
docker -version
```

### To check all the running containers on the host
 
```
docker ps
```

### To check all the non running and running containers on the host 

```
docker ps -a
```

### To count the number of images available on the host

```
docker images
```

### To run a particular docker image

```
docker run <image-name>
```

### To stop the container that was created

```
docker stop <container-name/container-id>
```

### To read the image used within the container 

```
docker ps -a
```

Check the image column for the particular container name 

### To delete all containers from docker host 
To perform this , first all the running containers must be stopped and all the containers must be deleted then using the particular command.

```
docker rm <container-id/container-name>
```

### To delete the entire docker image
Before deletion of the entire image , deletion of the container should take place.

```
docker rmi <image-name>
```

### To pull a docker image from docker hub to be used as a container later.

```
docker pull <image-name>
```

### To run a docker container with a custom name 

```
docker run --name <name> <container-name>
```




