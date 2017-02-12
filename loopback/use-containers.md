# The Backend

## Use Containers

Let us use a devops first approach. Our smallest experiments, no matter how trivial, will be closest to production best practices.

1. Login to your [cloud-box](../setup.md) over `ssh`. create it if you haven't done so already. It will make a robust environment for learning.
1. To start with a clean environment, run:
   ```
   mkdir -p ~/workspace
   cd ~/workspace
   rm -rf loopback-zero-to-hero
   ```
1. Step into the working directory:
   ```
   cd ~/dev/loopback-sandbox
   ```
1. Create a `Dockerfile` with the following content:

   ```
   # Use latest version 4.x of NodeJS
   # you can get details about the image from https://hub.docker.com/_/node/
   FROM node:4

   # install some useful tools
   RUN apt-get -y update
   RUN apt-get install -y tree
   RUN apt-get install -y vim

   # configure terminal access
   # https://github.com/dockerfile/mariadb/issues/3
   ENV TERM=xterm

   # configure envirnoment to work with tools used for tailing
   # https://github.com/jfrazelle/dockerfiles/issues/12
   ENV DEBIAN_FRONTEND=noninteractive
   RUN apt-get install -y less

   RUN mkdir -p ~/apps/loopback-zero-to-hero
   WORKDIR ~/apps/loopback-zero-to-hero
   ```

1. Create a `docker-compose.yml` file to install and run a reasonably up to date version of NodeJS:
   ```
   version: '2'
   services:
     loopback-mongo-sandbox:
       build:
         context: ./
       ports:
         - "3000:3000"
       volumes:
         - ~/workspace/loopback-zero-to-hero:/apps/loopback-zero-to-hero
   ```
1. Make sure to change the permissions to execute `sh` files:
   ```
   chmod 744 *.sh
   ```
1. Start the service: `docker-compose up`
