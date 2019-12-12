## DOCKER NETWORKING 

### THREE TYPES OF BASIC NETWORKS 

1. Bridge :- Bridge is the default network that is used when we run the `docker run <image-name>` command on the terminal. In this a docker container is separate from the docker host and to be accessible by any user, port mapping is implemented.

2. Host :- Host is the type of networking in docker which eliminates the use of port mapping as the docker container is directly linked with the docker host. However, multiple docker container can't be run with the Host network. To switch to the host network, use the following command : 
```
docker run <image-name> --network=host
```

3. None :- With the none network, the container is not connected to any other network or containers. This can be activated using the command :
```
docker run <image-name> --network=none
```

### USER-DEFINED NETWORKS 

* When one wants to create particular container running on a particular default network id , and you want to isolate other containers running on a different network id. To create internal network, it can be done by : 
```
docker network create --driver bridge  --subnet 182.18.0.0/16  custom-isolated-network
```
Here, we create another network id `182.18.0.0` and give it the name `custom-isolated-network`

### EMBEDDED DNS (Domain Name System)


* If in your docker host, a web server container and a sql container is running and you want to access the sql container you would do it as `mysql.connect(<internal address of mysql>)`. However this is not efficient, hence with docker you don't have to specify their internal address and can access by their name itself. The reason you can access a docker container by its name is because there is a DNS Server running on the docker host which stores the detail of each docker container. The DNS Server has its own unique internal address. 

### ADDITIONAL NOTES 

* To find all the networks within the docker host 
```
docker network ls 
```

* To inspect a particular network 
```
docker network inspect <network-name>
```
> Deploy a mysql database using the mysql image and name it mysql-db. Attach it to the newly created network wp-mysql-network
Set the database password to use db_pass123. The environment variable to set is MYSQL_ROOT_PASSWORD
```
docker run -d --name mysql-db --network=wq-mysql-network -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```

