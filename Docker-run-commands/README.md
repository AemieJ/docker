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

