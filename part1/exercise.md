## Part 1.1 Definitons and basic concepts
Most used commands
|command|explain|shorthand|
|:------|:------|:--------|
|`docker image ls`|Lists all images|`docker images`|
|`docker image rm <image>`|Removes an image|`docker rmi`|
|`docker image pull <image>`|Pulls image from a docker registry|`docker pull`|
|`docker container ls -a`|Lists all containers|`docker ps -a`|
|`docker container run <image>`|Runs a container from an image|`docker run`|
|`docker container rm <container>`|Removes a container|`docker rm`|
|`docker container stop <container>`|Stops a container|`docker stop`|
|`docker container exec <container>`|Executes a command inside the container|`docker exec`|
  
### __Exercise 1.1: Getting started__
Since we already did "Hello, World!" in the material let's do something else.
Start 3 containers from an image that does not automatically exit (such as nginx) in detached mode.
Stop two of the containers and leave one container running.
Submit the output for `docker ps -a` which shows 2 stopped containers and one running.<br>
__Command__
```
docker container run -d nginx
docker container run -d -it nginx
docker container run -d -it nginx
docker container ls
docker container stop f0 18
docker ps -a
```
__Output__
```
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS                      PORTS     NAMES
f00597f87827   nginx                           "/docker-entrypoint.…"   3 minutes ago   Exited (0) 32 seconds ago             gallant_sinoussi
184a93ec8a46   nginx                           "/docker-entrypoint.…"   3 minutes ago   Exited (0) 32 seconds ago             determined_goldstine
6a4f0ed525f3   nginx                           "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes                80/tcp    compassionate_lewin
```
### __Exercise 1.2: Cleanup__
We have containers and an image that are no longer in use and are taking up space. 
Running `docker ps -as` and `docker images` will confirm this.
Clean the docker daemon from all images and containers.
Submit the output for `docker ps -a` and `docker images`<br>
__Command__
```
docker container stop 6a
docker container prune
docker image prune -a
```
__Output__
```
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
```
### __EXERCISE 1.3: SECRET MESSAGE__
Now that we've warmed up it's time to get inside a container while it's running!
Image `devopsdockeruh/simple-web-service:ubuntu` will start a container that outputs logs into a file. Go inside the container and use `tail -f ./text.log` to follow the logs. Every 10 seconds the clock will send you a "secret message".
Submit the secret message and command(s) given as your answer.<br>
__Command__
```
docker run -d --rm -it --name ex13 devopsdockeruh/simple-web-service:ubuntu
docker exec -it ex13 bash
tail -f ./text.log
```
__Message__
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```



### EXERCISE 1.4: MISSING DEPENDENCIES
Start a Ubuntu image with the process `sh -c 'while true; do echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website; done'`<br>
If you're on Windows, you'll want to switch the `'` and `"` around: `sh -c "while true; do echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://$website; done"`.<br>
You will notice that a few things required for proper execution are missing. Be sure to remind yourself which flags to use so that the container actually waits for input.<br>
_Note also that curl is NOT installed in the container yet. You will have to install it from inside of the container._<br>
Test inputting `helsinki.fi` into the application. It should respond with something like
```html
<html>
  <head>
    <title>301 Moved Permanently</title>
  </head>

  <body>
    <h1>Moved Permanently</h1>
    <p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
  </body>
</html>
```
This time return the command you used to start process and the command(s) you used to fix the ensuing problems.<br>
**Hint** for installing the missing dependencies you could start a new process with `docker exec`.<br>
-This exercise has multiple solutions, if the curl for helsinki.fi works then it's done. Can you figure out other (smart) solutions?


### EXERCISE 1.5: SIZES OF IMAGES
In the Exercise 1.3 we used `devopsdockeruh/simple-web-service:ubuntu`.
Here is the same application but instead of Ubuntu is using Alpine Linux: `devopsdockeruh/simple-web-service:alpine`.
Pull both images and compare the image sizes. Go inside the alpine container and make sure the secret message functionality is the same. Alpine version doesn't have bash but it has sh.


### EXERCISE 1.6: HELLO DOCKER HUB
Run `docker run -it devopsdockeruh/pull_exercise`.
It will wait for your input. Navigate through Docker hub to find the docs and Dockerfile that was used to create the image.
Read the Dockerfile and/or docs to learn what input will get the application to answer a "secret message".
Submit the secret message and command(s) given to get it as your answer.


### EXERCISE 1.7: IMAGE FOR SCRIPT
We can improve our previous solutions now that we know how to create and build a Dockerfile.
Let us now get back to Exercise 1.4.
Create a new file on your local machine with and append the script we used previously into that file:
```
while true
do
  echo "Input website:"
  read website; echo "Searching.."
  sleep 1; curl http://$website
done
```
Create a Dockerfile for a new image that starts from ubuntu:20.04 and add instructions to install curl into that image. Then add instructions to copy the script file into that image and finally set it to run on container start using CMD.
After you have filled the Dockerfile, build the image with the tag "curler".
- If you are getting permission denied, use `chmod` to give permission to run the script.
The following should now work:
```
$ docker run -it curler

  Input website:
  helsinki.fi
  Searching..
  <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
  <html><head>
  <title>301 Moved Permanently</title>
  </head><body>
  <h1>Moved Permanently</h1>
  <p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
  </body></html>
```
Remember that _RUN_ can be used to execute commands while building the image!
Submit the Dockerfile.