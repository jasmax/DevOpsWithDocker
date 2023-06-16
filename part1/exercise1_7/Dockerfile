FROM ubuntu:20.04 

WORKDIR /mydir
RUN apt-get update && apt-get install -y curl

CMD while true; do echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website; done