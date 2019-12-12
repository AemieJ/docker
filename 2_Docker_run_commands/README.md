## DOCKER RUN COMMANDS 
> Terminal based 

### To run a particular container 
```
docker run <image-name> 
docker run <image-name>:latest
```

### To run a container with a particular version using a tag
```
docker run <image-name>:<tag>
```
### To run a simple prompt application using docker

Example: 
```
~/prompt-application$ ./app.sh
Welcome! Please Enter Your Name: Aemie

Hello and Welcome Aemie
```

```
docker run <application-name>

Hello and Welcome 
```

* To get docker in interactive mode for the application 
```
docker run -i <application-name>

Aemie 

Hello and Welcome Aemie
```

* To get docker running with the prompt application 
```
docker run -it <application-name>
Welcome! Please Enter Your Name: Aemie

Hello and Welcome Aemie
```

### Port mapping with docker 
In docker engine , there lies a docker container running its application at its port . However , for it to be accessible by the client , one needs to map the port from that of the docker container to that of docker engine.

Example: 
Docker webapp runs on port(Internal IP) : ```172.17.0.2``` while the internal IP of docker engine is ``` 192.168.1.5```.

```
docker run <application-name> 
```
If it is an application , it will run on port ```localhost:5000```.Hence to map the port from docker container to engine , use the following command: 

```
docker run -p 8080:5000 <application-name>
```
This application will run on the port ```192.168.1.5:8080``` and will be accessible.


### Volume mapping with docker

when we want to run databases such as MySQL which has data present inside ```/var/lib/mysql``` , once we stop the container from running all its data will be lost as well . If one wants to persist the data , we map the data of MySQL contain to another directory that is present outside the container but within the docker engine itself . This is accomplished by running the following command: 

```
docker run -v /opt/datadir:/var/lib/mysql mysql
```
This creates a copy of data in the directory ```/opt/datadir/``` and will contain the data even after you stop the container mysql and remove it.

### Inspect the container 
Returns the details of the contain in JSON format. 

```
docker inspect <container-name>
```
### Checking the logs of a container 

```
docker logs <container-name>
```


