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
[Dockerfile](exercise1_7/Dockerfile)<br>
__Command__
```
docker build . -t curler
docker run -it curler
```

### __EXERCISE 1.8: TWO LINE DOCKERFILE__
In this exercise create a Dockerfile and use FROM and CMD to create a brand new image that automatically runs server.<br>
[Dockerfile](exercise1_8/Dockerfile)<br>
__Command__
```
docker build . -t web-server
docker run web-server
```
__Output__
```
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
```

### __EXERCISE 1.9: VOLUMES__
Submit the command you used to complete the exercise.<br>
__Command__
```
docker run -d -v "C:/Users/User/Documents/mooc/devops with docker/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```

### __EXERCISE 1.10: PORTS OPEN__
Submit the command you used to complete the exercise.<br>
__Command__
```
docker run -p 9000:8080 devopsdockeruh/simple-web-service server
```

### __EXERCISE 1.11: SPRING__
Submit the Dockerfile you used to run the container.<br>
[Dockerfile](exercise1_11/Dockerfile)<br>
__Command__
```
docker build . -f Dockerfile -t spring-project
docker run -p 8080:8080 spring-project
```

### __EXERCISE 1.12: HELLO, FRONTEND!__
Submit the Dockerfile.<br>
[Dockerfile](exercise1_12/Dockerfile)
__Command__
```
docker build . -t example-frontend
docker run -it -p 5000:5000 example-frontend
```

### __EXERCISE 1.13: HELLO, BACKEND!__
Submit the Dockerfile and the command used.<br>
[Dockerfile](exercise1_13/Dockerfile)
__Command__
```
docker build . -t example-backend 
docker run -p 8080:8080 -it --rm example-backend
```

### __EXERCISE 1.14: ENVIRONMENT__
Submit the edited Dockerfiles and commands used to run.<br>
_frontend_
[Dockerfile](exercise1_14/frontend/Dockerfile)
_backend_
[Dockerfile](exercise1_14/backend/Dockerfile)
__Command__<br>
_frontend_
```
docker build . -t example-frontend -f Dockerfile-frontend
docker run -p 5000:5000 --rm -it example-frontend
```
_backend_
```
docker build . -t example-backend -f Dockerfile-backend
docker run --rm -it -p 8080:8080 example-backend
```


