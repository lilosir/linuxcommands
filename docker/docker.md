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


```docker container commit``` == ```docker commit```

```docker image build``` == ```docker build```


```dokcer image push``` == ```docker push```
```docker push [OPTIONS] NAME[:TAG]``` eg. ```docker push lilosir/hello-world:latest```

use https://hub.docker.com/_/registry to create a private image
