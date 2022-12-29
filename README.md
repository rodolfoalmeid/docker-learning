Docker-learning
================

## How to login to docker in the terminal

```
docker login --username:ralmeid
```
Then it will ask to type a password.

> __Note__
> Sometimes it is required to issue the commands using sudo


## How to create a docker image and push the image.

### Create a docker image

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

### Commit Changes to the Image

To commit changes to the image, we must first have the container ID. As with the example above, the `docker ps -a` command lists the ID as `3aee3f9bd45b`. We’re going to name our new image lamp-server-template and commit the changes with the command:

```
docker commit 3aee3f9bd45b lamp-server-template
```

If you run the `docker images` command, you’ll see the new image, lamp-server-template listed.

![image](https://user-images.githubusercontent.com/113181949/209955592-1a25ff6a-edbe-4013-8799-b3e2797895a1.png)

### Tag Your Image for Version Control

When you pull down an image from Docker Hub, the Status line includes the image tag as shown here:
```
Status: Downloaded newer image for ubuntu:latest
```

Docker tags are an easy way for you to know what version or release you are working with. This is especially useful for creating new images from a base image. For example, if you have a Ubuntu image you use as a base to create different images, Docker tags help you track the differences:
```
lamp-server-template:v1.8.10.2017
lamp-server-template:v2.8.10.2017
lamp-server-template:v3.8.10.2017
```

Create image tags with a docker commit. Using the example tags above, tag the new image with a version number and date:
```
docker commit 3aee3f9bd45b lamp-server-template:v1.8.0
```

Run `docker images` to see the new image created along with the associated tag:

![image](https://user-images.githubusercontent.com/113181949/209957013-389be021-b481-4907-86d3-2e365c58e20e.png)
