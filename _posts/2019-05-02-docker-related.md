---
layout: post
title:  "How to use docker command without 'sudo'"
date:   2019-05-02 08:40:00 +0800
categories: docker
---

### How to use docker command without 'sudo'?

#### issue 1
* err msg
```shell
ERROR: Couldn't connect to Docker daemon - you might need to run `docker-machine start default`.
```
* You should add your user in docker group. And then, you can use docker command without 'sudo'.

* template
```shell
$ sudo usermod -aG docker ${USER}
$ sudo service docker restart
```

* example
```shell
$ sudo usermod -aG root lance
$ sudo service docker restart
```
* Next, you have to logout in your OS. Finally, when you login, you can use docker command without 'sudo'.
```shell
logout
```
   
#### issue 2
* err msg
```shell
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/create: dial unix /var/run/docker.sock: connect: permission denied.
```
* (solution)[https://techoverflow.net/2018/12/15/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket/]


