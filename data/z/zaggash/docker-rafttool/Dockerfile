FROM golang:1.9 as build  
  
ENV CGO_ENABLED=0  
RUN go get github.com/docker/swarmkit/cmd/swarm-rafttool  
RUN go get github.com/docker/swarmkit/cmd/swarmctl  
  
FROM alpine:3.6  
COPY \--from=build /go/bin/swarmctl /bin/swarmctl  
COPY \--from=build /go/bin/swarm-rafttool /bin/swarm-rafttool  
COPY dump.sh /usr/local/bin/dump  

