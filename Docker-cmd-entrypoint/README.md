## DOCKER CMD AND ENTRYPOINT 

* In images such as ubuntu , when you run this image it immediately exits. The reason to why this happens is because in the dockerfile of every respective docker image , there is an instruction named `CMD` and this instruction is responsible for running. However for ubuntu, it uses `bash` as CMD and bash waits to see if there is anything associated with terminal , if not it exits. When the `docker run` command is used, docker doesn't associate with the terminal hence bash exits. To prevent this, we can change the CMD parameters. Let's say we want the image while running to sleep for 5 seconds.

```
Dockerfile 

CMD sleep 5 
//OR 
CMD["sleep", "5"]
```

* However, if one wants to explicitly change the parameters for sleep then it has to be done from terminal as such.
```
docker run ubuntu-sleeper sleep 10
```
But if the functionality of our image is to sleep for n seconds, it will be efficient to only specify the number of seconds from the terminal as such: 
```
docker run ubuntu-sleeper 10
```

* To accomplish this, one must use ENTRYPOINT within their dockerfile.
```
Dockerfile

ENTRYPOINT["sleep"]
```
Howver , if we specify no seconds from the terminal it will raise an error. Hence, we use CMD and ENTRYPOINT instructions together within the dockerfile.

```
Dockerfile 

ENTRPOINT["sleep"] 

CMD["5"]
```
> Here, the default sleep is for 5 seconds. Once can specify the number of seconds to change the default as well from the terminal.

* Now, if I want to use another command for the entrypoiint it can be done explicitly from the terminal by using the following command.
```
docker run --entrypoint sleep2.0 ubuntu-sleeper 10
```
