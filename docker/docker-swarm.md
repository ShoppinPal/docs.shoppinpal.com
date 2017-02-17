## Getting Started with Docker Swarm

A Docker swarm is a cluster of machines, all running docker which provides a scalable and reliable platform to run many containers.In this tutorial, we will be looking at how to setup a docker swarm.

**Note** : _Steps are documented below the video_.

{% youtube %} https://www.youtube.com/watch?v=L19VYdDWyIY&feature=youtu.be {% endyoutube %}

**Requirements** **:** 

1. Setup at 4 droplets on DigitalOcean.
2. Install docker\(version 1.13\) on each droplet using this shellScript. 
3. Name the droplets as numbers. for eg. swarm-00,swarm-01..so on.

![](/assets/docker/3.Final Setup.png)

**References used in this tutorial :**

1. [GitHub Repository](https://github.com/Bhushan001/docker-swarm-html) 
2. [Shellscript](https://gist.github.com/Bhushan001/857c2761fd6b85e072d6451c4c4a2d35) for installing latest vesrion on ubuntu
3. [Docker image](https://hub.docker.com/r/bhushangadekar01/docker-swarm-html/) of app to be deployed inside containers in docker swarm environment.

**Steps** **:**

1. Clone the Github repository in your local system using command :
   `git clone https://github.com/Bhushan001/docker-swarm-html.git`
2. Now you can go into the directory using: `cd docker-swarm-html`
3. Now you will need to copy file install.sh to all of your droplets using command.                                                                                 `scp install.sh root@ip_address:/root/install.sh`
4. after copying `install.sh` from local to droplets, you can install docker by executing script using : `./install.sh`
5. After successfully installing docker, you will need to setup docker swarm.
6. Log in into one of the droplets using ssh as `ssh root@ipaddressof_droplet `
7. To create docker swarm, run `docker swarm init --listen-addr ip-address-of-droplet:2377 --advertise-addr ip-address-of-droplet `this will _**initialize the docker swarm on this system and make this droplet as a swarm manager**_. This command will also generate a joining token for other droplets to join the swarm. copy that command and run it on each of the other droplets so they can join this swarm. 
8. You can use `docker node ls `to check how many nodes are there in the docker swarm.
9. Now you will need to deploy a service in this docker swarm.run the command                                                                         `docker service create --name website --publish 80:80 bhushangadekar01/docker-swarm-html `This will create a service in docker swarm from docker image **bhushangadekar01/docker-swarm-html **and run it as a container on port 80.

> Now you will be able to see your website running on port 80 of any of the droplets.** wait.**. **we deployed this service on only one droplet so how come it's available on every droplet?** because though there is only one service running the port that we deployed it on is mapped for every droplet in the swarm so when we hit port 80 on swarm-1 which does not have the service running it immediately knows which application we are trying to use and forwards our request to that host.

10 . Now when we want to deploy multiple instances of this application as a container we will use below command to deploy those many replicas of the container in docker swarm : `docker service update --replicas 10 website`  This will deploy 10 replicas of the container among the droplets in docker swarm.

   11.Now try shutting down one of the droplets in docker swarm, you will observe that though the containers on that droplet are terminated, those containers were redeployed on other droplets in the docker swarm. This increases the availability and scalability of our application in the production.









