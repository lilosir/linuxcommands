```FROM```  will declare the base image

```LABEL``` define image metadata, like comments
```
LABEL maintainer="sryoliver@gmail.com"
LABEL version="1.0"
LABEL description="......"
```

```RUN``` run anything from the os image. It will add a new image layer every time you run RUN, so it is better to combine all the RUN comand into one line. Use \ to return a new line.
```
RUN yum update && yum install -y vim \n
    python-dev
```
```
RUN apt-get update && apt-get install -y perl \
    pwgen --no-install-recommends && rm -rf \
    /var/lib/apt/lists/*           #delete cache
```
```
RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'
```

```WORKDIR``` go to a dicrectory, like ```cd``` in linux, but don not use ```RUN cd```, and please use absolute path
```
WORKDIR /test       #it will ceate test folder if it not exists
WORKDIR demo
RUN pwd             #print /test/demo
```

```ADD``` and ```COPY``` both of them will copy a file to dest path. In most senarios, ```COPY``` is better than ```ADD```. ```ADD``` also can unzip file. If you want to add remote file/directory, please use ```RUN curl``` or ```RUN wget```!
```
ADD hello /
```
```
ADD test.tar.gz /    #will add to root and unzip, COPY will not
```
```
WORKDIR /root
ADD hello test/       #/root/test/hello
```

```ENV``` set constants
```
ENV MYSQL_VERSION 5.6    #set mysql version
RUN apt-get install -y mysql-server="${MYSQL_VERSION}" \
    && rm -rf /var/lib/apt/lists/*            #use the constant
```

```CMD``` provides defaults for an executing container, there can only be one ```CMD```, if you list more than one ```CMD```, only the last one will take effect. If the user specifies arguments to ```docker run``` then they will override the default specified in ```CMD```. ```RUN``` actually runs a command and commits the result; ```CMD``` does not execute anything at build time, but specifies the intended command for the image.

```ENTRYPOINT``` allows you to configure a container that will run as an executable, and never gonna be igbored.
