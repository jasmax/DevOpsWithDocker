### __Exercise 2.1: __
Submit the docker-compose.yml, make sure that it works simply by running docker compose up if the log file exists.<br>
[Dockerfile](part2/exercise2_1/docker-compose.yml)<br>
__Command__
```
docker compose up
```
__Output__
```
[+] Building 0.0s (0/0)
[+] Running 2/2
 ✔ Network ex2_1_default         Created                                                     0.4s 
 ✔ Container simple-web-service  Created                                                     1.3s 
Attaching to simple-web-service
simple-web-service  | Starting log output
simple-web-service  | <nil>
simple-web-service  | open /usr/src/app/text.log: is a directory
simple-web-service  | <nil>
```
