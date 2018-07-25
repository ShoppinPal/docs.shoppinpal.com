# Use Containers

## Use Containers

Let us go with a `devops-first` approach:

> Our smallest experiments, no matter how trivial, will be closest to production best practices!

_**Note**: Even without the video, you can learn all the crucial details from the steps that are documented below_

{% embed data="{\"url\":\"https://youtu.be/u1CG-ujpnWk\",\"type\":\"video\",\"title\":\"\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/u1CG-ujpnWk/maxresdefault.jpg\",\"width\":1280,\"height\":720,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/u1CG-ujpnWk?rel=0&showinfo=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/u1CG-ujpnWk?rel=0&amp;showinfo=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}

1. Login to your [cloud-box](../1.-the-ideal-workspace/setup-a-machine-in-the-cloud/setup-box-on-digitalocean/) over `ssh`.
   * Create it if you haven't done so already.
   * This will be a robust environment for learning.
2. To start with a clean environment, run:

   ```text
   mkdir -p ~/workspace && \
   cd ~/workspace && \
   rm -rf loopback-zero-to-hero && \
   mkdir -p ~/workspace/loopback-zero-to-hero && \
   cd ~/workspace/loopback-zero-to-hero
   ```

3. [Setup your IDE](../appendix/project-sync-via-ide/sftp-with-webstorm.md#steps-are-documented-below-the-video) to work with the remote directory on the cloud-box.
   1. **Create New Project named** `loopback-zero-to-hero`
   2. **For** `Deployment Path` **use** `/root/workspace/loopback-zero-to-hero`
4. In your IDE, create a `Dockerfile` with the following content:

   ```text
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

5. Create a `docker-compose.yml` file to install and run a reasonably up to date version of NodeJS:

   ```text
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

6. Start the service: `docker-compose up` and after it finishes running, you should see something like the following at the very end:

   ```text
   WARNING: Image for service loopback-zero-to-hero was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
   Creating loopbackzerotohero_loopback-zero-to-hero_1
   Attaching to loopbackzerotohero_loopback-zero-to-hero_1
   loopbackzerotohero_loopback-zero-to-hero_1 exited with code 0
   ```

