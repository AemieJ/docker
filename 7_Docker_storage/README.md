## DOCKER STORAGE 

### FILE SYSTEM

* When docker is first installed, it is stored in `/var/lib/docker` folder and all the respective folders are already built in it. We have talked about the layer architecture when we build a docker image. This layer architecture is stored within the `Image Layers` and is READ-ONLY. Hence, modifications can not be made to it. When you use `docker run` , a `Container Layer` is formed which READ-WRITE and the modifications to it will be destroyed as soon as the image has been stopped from running. 

* Also, if you have a particular application in your image layer, it is accessible by all the other containers and when modifications are supposed to be made on it, a copy of it is stored in the container layer and you can modify it however you can only save the changes while building it, however if the changes are not saved and you destroyed the docker image from running all modifications are lost.

* However, if you wish to persist this data, you create a volume using ``` docker volume create data_volume``` command , in the `/var/lib/docker/` , the volume folder created has the following structure `/var/lib/docker/volumes/data_volume` .

* Hence let's say I want to persist the data of mysql in the image layer and all the changes I modify while running mysql in the container layer. I can do this by using the following command : 
```
docker run -v data_volume:/var/lib/mysql mysql
```

* Now let's say I don't want to create a volume before running the image to use it. Hence if you create another data_volume2 within the docker volume, docker will automatically create this instance for you without the need for creating it explicitly. This is called Volume Mounting. 

### ADDITIONAL NOTE

* To use -v param is old style, hence for volume mounting you use the --mount param in the following way : 
```
docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```

* Storage drivers are responsible for handling the layer architecture and docker chooses the most suitable storage drivers based on your operating system.
