# DevOps with Docker (University of Helsinki MOOC)
https://devopswithdocker.com/

**Part 1.1 Definitons and basic concepts**
*Exercise 1.1: Getting started
Since we already did "Hello, World!" in the material let's do something else.
Start 3 containers from image that does not automatically exit, such as nginx, detached.
Stop 2 of the containers leaving 1 up.
Submit the output for docker ps -a which shows 2 stopped containers and one running.*

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

*Exercise 1.2: Cleanup
We've left containers and a image that won't be used anymore and are taking space, as docker ps -as and docker images will reveal.

Clean the docker daemon from all images and containers.

Submit the output for docker ps -a and docker images*

C:\Users\User>docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

C:\Users\User>docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
