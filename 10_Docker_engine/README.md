## DOCKER ENGINE

* When you initially install docker on your os, during that span 3 components namely `Docker CLI`, `REST API` and `Docker Daemon` are installed.

1. Docker Daemon : is a background process that manages the docker objects such as images, containers, etc.
2. REST API : is the API interface used to provide instruction to daemon.
3. Docker CLI : Command line interface. 

> Docker CLI could be on another host and can still work with the `Docker Engine` using `docker -H=remote-docker-engine:2375`. Here 2375 is the port number. To run any container, let's say for instance nginx, we can do it by using the command `docker -H=10.123.2.1:2375 run nginx` 

### CONTAINERIZATION DONE USING NAMESPACES 

* Namespace Isolation Technique (Process ID) : When a linux os boots up, the root processes runs with their own PID, after botting up several processes start running and each of them have a unique PID's. Let's say for instance we have Child System( Container) within the Linux System. 

```
LINUX SYSTEM 
PID1
PID2
PID3
PID4
```

Here, linuz has 4 unique PID, then within the container it has its own PID's.

```
CHILD SYSTEM
PID1
PID2
```

However, each PID is meant to be unique. This is where namespaces come into role. The child system PIDs are mapped to Linux system PIDs as PID5 AND PID6 respectively.

### cgroups 

* Each container within the docker host makes use of the same memory and cpu and there is no limitations as to how much resource a container can use. Hence, to restrict the amount of resources provided to any container, we make use of cgroups. 

```
docker run --cpus=0.5 <container-name>
docker run --memory=100m <container-name>
```

Here, it makes sure that the particular container can't use more than 50% of cpu resources and not more than 100MB of memory. 
