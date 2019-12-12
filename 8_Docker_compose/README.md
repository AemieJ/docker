## DOCKER COMPOSE 

### VOTING APP STRUCTURE 

1. voting-app (python)
2. in-memory DB(redis)
3. worker(.NET)
4. db(PostgreSQL)
5. result-app(NodeJS)

### IMPLEMENTATION OF STRUCTURE USING DOCKER RUN AND LINK 

```
docker run -d --name=redis redis
docker run -d --name=db postgres:9.4
docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
docker run -d --name=result -p 5001:80 --link db:db result-app
docker run -d --name=worker --link db:db --link redis:redis worker
```

Without the link param, docker will not know with what databases and worker the application must run with. Hence, link must be included.

### IMPLEMENTATION OF STRUCTURE USING DOCKER COMPOSE 

* When the particular images are not there on docker hub and we have built those applications, hence we use the build 
for the vote, result and worker application.

```
docker-compose.yml
redis:
	image: redis
db: 
	image: postgres:9.4
vote: 
	build: ./vote
	ports:
	     - 5000:80
	links:
	     - redis
result: 
	build: ./result
	ports:
   	     - 5001:80
	links:
	     - db
worker: 
	build: ./worker
	links:
	     - db
	     - redis
```
To run this use ```docker-compose up```
This is version-1 however it had some limitations. You couldn't include the network you wanted to change for the image.

### VERSION-2 OF DOCKER COMPOSE 

* In version-2, you can included a dedicated network and docker will then automatically create the links between all the services hence eliminating the use of links.

```
docker-compose.yml
version: 2
services:
   redis:
	image: redis
   db: 
	image: postgres:9.4
   vote: 
	build: ./vote
	ports:
	     - 5000:80
	depends_on:
             - redis
   result: 
	build: ./result
	ports:
   	     - 5001:80
   worker: 
	build: ./worker
```
> Note: We can create a separate front-end and back-end network(in case of redis and db).voting and result should include both front-end and back-end. The modified yml file is not used for development purposes. 

### VERSION-3 OF DOCKER COMPOSE 

* The version 3 supports with docker swarn.

```
docker-compose.yml
version: 3 
services:
   redis:
	image: redis
   db: 
	image: postgres:9.4
   vote: 
	build: ./vote
	ports:
	     - 5000:80
	depends_on:
             - redis
   result: 
	build: ./result
	ports:
   	     - 5001:80
   worker: 
	build: ./worker

```
