## DOCKER REGISTRY 

* It's the central repository of all docker containers.
* When you run a particular container using `docker run` that image is pulled from the docker hub. The structure of the image is given as <docker registry>/<author/user>/<image name>. Hence, when you run `docker run nginx`, the image name is assumed to be samed as the organization/author hence it is the same as `docker run nginx/nginx`. Also, all these images are stored in a public repository given as `docker.io` (Docker Hub). There are other registry which are public.

* There are private registry such as AWS. However, to access the image from a private registry you need to first login in the docker using `docker login`, after you've successfully passed the credentials, only then you can pull an image from the registry.

### DEPLOY PRIVATE REGISTRY

* Even if AWS and other platforms provide private registry on an account with them, however there might be times you want to deploy to your own private registry
* The docker registry is itself as an another application and is available from docker hub and runs on `localhost:5000`, hence to push your image on this registry, do the following command : 

```
docker run -d -p 5000:5000 --name registry registry:2

docker image tag my-image localhost:5000/my-image
docker push localhost:5000/my-image

```

* To pull the image from this private registry, it is done by : 

1. Running from your own local machine.
```
docker pull localhost:5000/my-image
```

2. If accessing this image from another host, it is done by including the ip address.
```
docker pull 192.168.56.100:5000/my-image
```

