## DOCKER IMAGES 

### Why would you want to containerise your own docker image ? 

* The docker image that you're expecting is not available on docker hub.
* You and your team have created an application and want to make a docker image for deployment purpose.

### How to containerise ? 

* To containerise a docker image , one needs to create a dockerfile. A dockerfile is a layered architecture which is divided into instruction followed by arguments. 

* Example , if one wants to run a flask application , there are several instructions to be followed which includes : 

```
Layer 1. Base ubutun layer(or any image or os you're initially extracting from)
Layer 2. Changes in apt packages
Layer 3. Changes in pip packages
Layer 4. Source Code(copy into the dockerfile)
Layer 5. Update Entrypoint with Flask Command
```
The dockerfile for the respective layer architecture will be as followed :

```
Dockerfile 

FROM Ubuntu

RUN apt-get update && apt-get -y install python
RUN pip install flask flask-mysql

COPY ./opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

* To build the docker image from the dockerfile , the following command is used from the terminal : 

```
docker build Dockerfile -t simple-flask-app .
```

### Failure in build 

* Even at a particular step , if the docker build fails (let's say at layer 3) then when you rerun the docker build the first 2 layers are already built and resumes from the third layer.

### YOU CAN CONTAINERISE EVERYTHING.
