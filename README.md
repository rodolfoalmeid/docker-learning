Docker-learning
================

## How to login to docker in the terminal

```
docker login --username:ralmeid
```
Then it will ask to type a password.

> __Note__
> Sometimes it is required to issue the commands using sudo


## How to create a docker image

In this example we will use latest ubuntu image.

1. Pull the latest Ubuntu image:

```
 docker pull ubuntu
```

2. Create the new container, such that we can add our LAMP stack to Ubuntu. This example names the container lamp-server-template and adds the bash option to the docker command to enter the container in order to continue making changes:


```
docker run --name lamp-server-template -it ubuntu:latest bash
```
3. Into the bash update and upgrade the ubuntu image.

```
apt update

apt upgrade
```

4. Install the lamp-server metapackage inside the container:

```
apt-get install lamp-server^
```

This upgrade and installation will take longer than it would if you were working on a standard server. During the installation of the LAMP stack, you will be prompted to create a MySQL root user password. When the installation completes, exit the container:
```
exit
```

Use `docker ps -a` to list all of the available containers:

![image](https://user-images.githubusercontent.com/113181949/209954433-b9e6f1f6-7c2a-4b11-9d67-a4a44ec47e84.png)

