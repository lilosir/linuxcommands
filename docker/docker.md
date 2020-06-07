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


### docker network bridge

```docker run ... --link [contianer name]``` will add Add link to another container, it is like add DNS to the current container, if `ping` the linked container name, it will `ping` the linked container's IP address. But it is single direction. 

By default, if we do not set netowrk, container will run in default network, `bridge(eth0)`, to access internet. We can use link command to link one container to another one. but in real life, the ideal way is connecting containers to the same network, so they can communicate with each other, instead of link every containers. First, we can use ```docker network create -d bridge my-bridge``` to create a network, which is a driver. Once we run docker with ```--network my-bridge```, so the container will connect to `my-bridge` this network. Use ```docker network inspect [network name]``` to see which containers are connected to this network. In our custome network, all the containers are linked already, but for the default is not. We also can use ```docker network connect [network name] [container name]``` to add container to a network. ps, container can be in multiple networks. 

``` docker run ... -p 80(container service port):80(host port) ...``` `-p` is publishing container's port to the host. For example, we run a nginx on a linux kernal without `-p`, the nginx will be connected to the default network bridge, and create an IPv4Address inside of the default network. but the linux eth0 cannot access this web server. If add `-p`, this option will redicrect all the network data to nginx container. Let's say the linux has a public ip address(AWS), if we access the public ip address with the port, we can access the nginx web server

### docker network none
```--network [network]```, the [network] can be `none`(preset internal network), this network has no loopback, which means, if the container has been connected to none network, the only way to access it is ```docker exec -it [container name] /bin/sh```. It is kinkda closed network. Maybe for some confidential operations?

### docker network host
the container is connected to host network. if run ```ip a``` we can find the state is same as run ```ip a``` in the host linux terminal. 
