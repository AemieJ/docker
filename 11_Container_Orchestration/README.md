## CONTAINER ORCHESTRATION 

### WHy orchestrate ? 

* For instance, when we run `docker run nodejs`, it is running on our docker host. But what if user increases and the particular container is not able to handle the host, you need to add aditional container( instances ). If during this time, if the container fails, it should be detected and be replaced by an additional instance again. However, if the docker host becomes inaccessible and so does all the containers/instances. So we use orchestration to solve this issue. 

### ORCHESTRATE 

* With this it provides certain tools and scripts that can help host containers in a production env. Even if an instance fails, it will still continue running. 
* Orchestration can automatically create more instances if the number of user increases and decrease when number of user decreases. ALso when the load is too hard to bear, container orchestration automatically adds docker host and creates a complex networking to link all these docker hosts with instances. 

> Docker swarn( by Docker), kubernetes( by Google), MESOS are the ochestration solutions. kubernetes is considered to be the most popular among all.

### DOCKER SWARM 

* SETUP SWARM 

1. To setup, initially you need to have docker host(s) installed on your machine. 
2. One host is designated as the `Swarm Manager` while others are workers.
3. Run `docker swarm init` in the Swarm Manager.
4. On the workers, then run `docker swarm join --token <token>

* DOCKER SERVICES 

They are one or more instances of a single application or service that runs through the workers( node ) of the cluster.
To run the instance of a container in the workers( node ), you create a docker service in the swarm manager where `replicas` specify the number of instances you require to distribute among all the workers( docker host ).

```
docker service create --replicas=3 <container-name>
``` 
Here, I distribute the instance into 3 workers.


### KUBERNETES 

* With the kubernetes CLI( kubectl), you can even run upto 1000 instances of your container and with this, you can even automatically control whether the number of instances to be distributed should be high or low based on the load of users. 

```
kubectl run --replicas=1000 <container-name> 

kubectl scale --replicas=2000 <container-name> //automatic scaling
kubectl rolling-update <container-name> --image=<image name>:tag //upgrade these 2000 instances using rolling fashion 
kubectl rolling-update <container-name> --rollback //In case of failure, you can always roll-back 

```

* kuberentes uses docker host to host applications using docker containers and it needn't be docker always. kubernetes includes nodes and a couple of node forms the kubernetes cluster. The information about all the cluster is stored in the master and is responsible for the orchestration. 

* When you install kubernetes on your local machine, you're installing the following : 
1. API Server : acts as the front-end for kubernetes. 
2. etcd : is a distributive key value store used to store all the datas to manage the cluster.To avoid conflicts between multiple masters is one of its job.
3. kubelet : The agent that runs on each node in the cluster. It is responsible to make sure that nodes are running as expected. 
4. Container runtime( like docker )
5. Controller : responsible for noticing and responding when nodes or containers go down. (brain behind orchestration)
6. Scheduler : responsible for distributing work among multiple nodes.

