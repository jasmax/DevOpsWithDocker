# [DevOps with Docker (University of Helsinki MOOC)](https://devopswithdocker.com/)

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
  
#### Exercise 1.1: Getting started
Since we already did "Hello, World!" in the material let's do something else.
Start 3 containers from an image that does not automatically exit (such as nginx) in detached mode.
Stop two of the containers and leave one container running.
Submit the output for `docker ps -a` which shows 2 stopped containers and one running.
```console
C:\Users\User>docker container run -d nginx
6a4f0ed525f3b89bc83a5658dde177ddd6a8cdbeb2d509648a1286117f4935b0
C:\Users\User>docker container run -d -it nginx
184a93ec8a46ce613708577485c42bb94728a6e42cbc686f34a4ad6874eccece
C:\Users\User>docker container run -d -it nginx
f00597f878273aad88a45d1be39236ad56d8dc0ea4d8fdc6ab00bc954f9189a7
C:\Users\User>docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
f00597f87827   nginx     "/docker-entrypoint.…"   24 seconds ago   Up 21 seconds   80/tcp    gallant_sinoussi
184a93ec8a46   nginx     "/docker-entrypoint.…"   31 seconds ago   Up 29 seconds   80/tcp    determined_goldstine
6a4f0ed525f3   nginx     "/docker-entrypoint.…"   5 minutes ago    Up 5 minutes    80/tcp    compassionate_lewin
C:\Users\User>docker container stop f0 18
f0
18
C:\Users\User>docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
6a4f0ed525f3   nginx     "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes   80/tcp    compassionate_lewin
C:\Users\User>docker ps -a
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS                      PORTS     NAMES
f00597f87827   nginx                           "/docker-entrypoint.…"   3 minutes ago   Exited (0) 32 seconds ago             gallant_sinoussi
184a93ec8a46   nginx                           "/docker-entrypoint.…"   3 minutes ago   Exited (0) 32 seconds ago             determined_goldstine
6a4f0ed525f3   nginx                           "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes                80/tcp    compassionate_lewin
```
#### Exercise 1.2: Cleanup
We have containers and an image that are no longer in use and are taking up space. 
Running `docker ps -as` and `docker images` will confirm this.
Clean the docker daemon from all images and containers.
Submit the output for `docker ps -a` and `docker images`
```console
C:\Users\User>docker container stop 6a
6a
C:\Users\User>docker container rm f0 18 6a
f0
18
6a
C:\Users\User>docker rmi nginx hello-world
Untagged: nginx:latest
Untagged: nginx@sha256:0047b729188a15da49380d9506d65959cce6d40291ccfb4e039f5dc7efd33286
Deleted: sha256:1403e55ab369cd1c8039c34e6b4d47ca40bbde39c371254c7cba14756f472f52
Deleted: sha256:0274f249eda4c376bde7cbe0b719ea3aef10201846d7262f37f7a0fc0b4fcf90
Deleted: sha256:e01fc49cb889c5dd6b11390e9863ba00f886315c5a403ee5955fb5c88d2aa576
Deleted: sha256:b2a367ee540c5d40c704fdece005b422f55f85a61b96a25bd99d6847669958a0
Deleted: sha256:2c1c6d39cbcc4767b0798aacc03f203951057e77c5edebca1fdfbcd4997f2919
Deleted: sha256:d260638126e1d2d3202dec36b67f124624fbcdad3afedd334e7260bf75dad8da
Untagged: hello-world:latest
Untagged: hello-world@sha256:94ebc7edf3401f299cd3376a1669bc0a49aef92d6d2669005f9bc5ef028dc333
Deleted: sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412
Deleted: sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359
C:\Users\User>docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
C:\Users\User>docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
```
