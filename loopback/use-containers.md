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
   1. Open **Webstorm IDE &gt; Tools &gt; Deployment &gt; Configuration**   
      This will open the configuration window where you will be adding a server .
   1. Click on "**+**" Symbol i.e.** Add Deployment Server**
   1. Now In** Connection tab** ,Specify The Name You want to give to this deployment server. For eg. **Webstorm Remote Access**
   1. Now Select Type: `SFTP`
   1. Now Specify other details as :   
      1. **Host** : mention the IPv4 address of your droplet.
      2. **port** : 22
      3. **rootpath**: / \(this specifies root path of your droplet\)
      4. **username**:username for loggin into your droplet. For eg. root
      5. **password**: your password
   7. Additionally click on "**Test SFTP Connection**" to verify if your connection is authorized or not.
   8. Once your connection is successful,Navigate to** Mappings tab **.
      1. **Local Path** : path of your application in your system
      2. **Deployment Path** : path of your application on the remote host. For eg. /root/dev/BluBox where BluBox is the application directory.
   9. Additionally we can chose to ignore few directories which we want i.e.node modules\_,\_bower\_components etc. by adding them to excluded paths.
   10. Now Click on **OK**.
   11. Your Webstorm Deployment Server Configuration is complete.
   12. Now Click on **Tools &gt; Deployment**  and select **Sync with Deployed to Webstorm Remote Access.**
   13. It will take some time to sync local project with the remote one.
   
   14. after synchronization, select **automatic upload** from **tools &gt; deployment** menu.
   
   15. Now whenever you save changes, **the code is uploaded on the remote host and application is re-deployed with the updated code.**


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
1. Start the service: `docker-compose up`
