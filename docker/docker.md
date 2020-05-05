`docker container ls -a` == `docker ps -a`

`docker ps -aq` will group only show contianer id

`docker rm $(docker container ps -aq)` 

```
FROM scratch
Add hello /
CMD ["/hello"]
```
===> ```docker build -t [name] .```
hello is a binary executable file

```
FROM centos
RUN yum install -y vim
```
===> `docker build -t [name] .`


```docker container commit``` == ```docker commit``` ```docker container stop``` == ```docker stop``` 

```docker image build``` == ```docker build```


```dokcer image push``` == ```docker push```
```docker push [OPTIONS] NAME[:TAG]``` eg. ```docker push lilosir/hello-world:latest```

use https://hub.docker.com/_/registry to create a private image


The ```docker exec``` command runs a new command in a running container.

### ```docker run```

```--memory=200M``` allocate memory, at most 200M

```--cpu-shares=2``` run cpu shares which is relative weight, for example, container A runns with cup-shares=2, container B runs with 4, container A will take 33% cpu while container B takes 66%

##### in linux, use ```veth``` (peer to peer pair), to connect two namespaces to communicate with each other. Same theroy, in docker, there is a ```docker0``` bridge, which can use veths to connect every containers, that is why containers can talk with each other. Also, docker0 => NAT => eth0(ip address) => internet, that is why containers can access network.
