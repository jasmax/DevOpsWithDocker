### __Exercise 1.1: Getting started__
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

### __EXERCISE 1.4: MISSING DEPENDENCIES__
This time return the command you used to start process and the command(s) you used to fix the ensuing problems.<br>
__Command__
```
docker run -it --name missdep ubuntu sh -c "apt update; apt install -y curl; echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://$website;"
```

### __EXERCISE 1.5: SIZES OF IMAGES__
Pull both images and compare the image sizes. Go inside the alpine container and make sure the secret message functionality is the same.
__Command__
```
docker pull devopsdockeruh/simple-web-service:ubuntu
docker pull devopsdockeruh/simple-web-service:alpine
```
__Image size__
```
docker images
REPOSITORY                          TAG       IMAGE ID       CREATED        SIZE
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   2 years ago    83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   2 years ago    15.7MB
```
__Command__
```
docker run -d -it devopsdockeruh/simple-web-service:alpine
docker exec -it c8e sh
tail -f ./text.log
```
__Message__
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

### __EXERCISE 1.6: HELLO DOCKER HUB__
Submit the secret message and command(s) given to get it as your answer.<br>
__Command__
```
docker run -it devopsdockeruh/pull_exercise
```
__Message__
```
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

### __EXERCISE 1.7: IMAGE FOR SCRIPT__
Submit the Dockerfile.<br>
[Dockerfile](part1/exercise1_7/Dockerfile)<br>
__Command__
```
docker build . -t curler
docker run -it curler
```