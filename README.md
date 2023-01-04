Docker-learning
================

------------------------------------------

# Table of Contents

1. [How to login to docker in the terminal](#how-to-login-to-docker-in-the-terminal)
2. [How to create a docker image and push the image to Dockerhub](#how-to-create-a-docker-image-and-push-the-image-to-dockerhub)
3. [How to push images to Google Cloud](#how-to-push-images-to-google-cloud)


---------------

## How to login to docker in the terminal

```
docker login --username:ralmeid
```
Then it will ask to type a password.

> __Note__
> Sometimes it is required to issue the commands using sudo


## How to create a docker image and push the image to Dockerhub

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

### Push Your Image to Docker Hub

Before pushing the image to Docker Hub, add a description, your full name (FULL NAME in the example here), and Docker Hub username (USERNAME) in the docker commit:
```
docker commit -m "Added LAMP Server" -a "FULL NAME" d09dd0f24b58 USERNAME/lamp-server-template:v1.8.10.2017
```

Once this is fully tagged, log in and push it to Docker Hub:
```
docker login docker.io
```

You will be prompted for your Docker Hub credentials. When authentication succeeds, you will see Login succeeded. 

![image](https://user-images.githubusercontent.com/113181949/209959895-75b9a915-6077-4076-ab77-3e03ee231fe3.png)

Check the image repository with the command

```
docker images
```
![image](https://user-images.githubusercontent.com/113181949/209959739-b6ea92de-1dc1-4cc8-91b0-b7416e9ddb92.png)

Now, you can push the image to the Hub with the command:

```
docker push rralmeid/lamp-server-template:v1.8.0
```
![image](https://user-images.githubusercontent.com/113181949/209959988-7ee22fa4-4500-45b7-b7d9-206771d02070.png)


Open a browser, log in to your Docker Hub account, and go your main repository. You will see the new image listed. Click on the image and then click on the Tags tab to see the added tag:

Our image, complete with tags, on Docker Hub

![image](https://user-images.githubusercontent.com/113181949/209960783-1ab04815-e320-4f62-8837-55d963fd83f3.png)

How to push images to Google Cloud
==================================

Requirements:
- Install Docker in your computer
- Set up a Google Cloud account and Project.



1 - Login to google repository

Login if using the old gcr.io
```
sudo cat neuvector-373118-2dd92e80c2ea.json | sudo docker login -u _json_key --password-stdin https://gcr.io
```

Login if using the new artifact Registry
```
sudo cat neuvector-373118-2dd92e80c2ea.json | sudo docker login -u _json_key --password-stdin https://us-docker.pkg.dev  
```

2 - Push image

Push images to gcr.io repository.
```
sudo docker push gcr.io/lofty-chemist-373111/lamp-server-template
```

Push images to Artifact repository.
```
sudo docker push us-docker.pkg.dev/neuvector-373118/gcr.io/ubuntu
```
