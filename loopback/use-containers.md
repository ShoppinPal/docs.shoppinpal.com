# The Backend

## Use Containers

Let us go with a `devops-first` approach:
> Our smallest experiments, no matter how trivial, will be closest to production best practices!

1. Login to your [cloud-box](../setup.md) over `ssh`.
   * Create it if you haven't done so already.
   * This will be a robust environment for learning.
1. To start with a clean environment, run:
   ```
   mkdir -p ~/workspace && \
   cd ~/workspace && \
   rm -rf loopback-zero-to-hero && \
   mkdir -p ~/workspace/loopback-zero-to-hero && \
   cd ~/workspace/loopback-zero-to-hero
   ```
1. [Setup your IDE](../configuring-webstorm-ide-for-code-deployment-on-remote-host.md#steps-are-documented-below-the-video) to work with the remote directory on the cloud-box.
   1. **Create New Project named `loopback-zero-to-hero`**
   2. **For `Deployment Path` use `/root/workspace/loopback-zero-to-hero`**
1. In your IDE, create a `Dockerfile` with the following content:
   ```
   # Use latest version 4.x of NodeJS
   # https://hub.docker.com/_/node/
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

   RUN mkdir -p /apps/loopback-zero-to-hero
   WORKDIR /apps/loopback-zero-to-hero
   ```

1. Create a `docker-compose.yml` file to install and run a reasonably up to date version of NodeJS:
   ```
   version: '2'
   services:
     loopback-zero-to-hero:
       build:
         context: ./
       ports:
         - "3000:3000"
       volumes:
         - ~/workspace/loopback-zero-to-hero:/apps/loopback-zero-to-hero
   ```
1. Start the service: `docker-compose up` and after it finishes running, you should see something like the following at the very end:
   ```
   WARNING: Image for service loopback-zero-to-hero was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating loopbackzerotohero_loopback-zero-to-hero_1
Attaching to loopbackzerotohero_loopback-zero-to-hero_1
loopbackzerotohero_loopback-zero-to-hero_1 exited with code 0
   ```
