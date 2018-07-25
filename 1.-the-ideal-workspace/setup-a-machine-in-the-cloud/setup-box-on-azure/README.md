# Setup box on Azure

## Setup box on Azure

1. Login to Azure and [create a machine](https://shoppinpal.gitbook.io/docs-shoppinpal-com/~/edit/drafts/-LIEPfiso_7iB9aIXIZ0/1.-the-ideal-workspace/setup-a-machine-in-the-cloud/setup-box-on-azure/create-a-machine-on-azure)
   1. You can use a personal account to do this, or
   2. request access to your company's account, or
   3. ask your company's devops team to do this on your behalf.
2. After the new machine is ready, make sure:
   1. You know its IP address.
   2. _Optionally_, we recommend that you map your `<machine-ip>` to a friendly domain name like `<myName-cloud-box-1.domain.com>`
      1. If you have a CloudFlare account, use it.
      2. **Configure cloudflare for DNS only. Bypass any HTTP related CDN.**
      3. This may take some time to take effect and will hopefully be ready for you to use by the time you finish rest of the steps.
3. Use `ssh` to login:
   1. either: `ssh <username>@<machine-ip>`
   2. or: `ssh <username>@<myName-cloud-box-1.domain.com>`
4. Install `docker-compose` on your cloud box. You can copy-paste the following script, which is a multi-line command and it will "just work."

   ```text
   sudo apt-get update && \
   sudo apt-get --assume-yes install apt-transport-https ca-certificates && \
   sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D  && \
   echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list && \
   sudo apt-get update && \
   sudo apt-get --assume-yes install tree && \
   sudo apt-get --assume-yes install mosh && \
   sudo apt-get --assume-yes install docker-engine && \
   echo "alias deleteContainers='docker rm \$(docker ps -a -q)'" >> ~/.bash_aliases && \
   echo "alias removeImages='docker rmi \$(docker images -f "dangling=true" -q)'" >> ~/.bash_aliases && \
   sudo service docker start && \
   LATEST=$(
   sudo curl -sSI https://github.com/docker/compose/releases/latest |
    tr -d '\r' |
    awk -F'/' '/^Location:/{print $NF}'
   ) && \
   sudo curl -L "https://github.com/docker/compose/releases/download/${LATEST}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
   sudo chmod +x /usr/local/bin/docker-compose && \
   docker-compose --version
   ```

5. At this point you have a powerful and scalable setup. We will put it to good use as we explore various exercises in this training guide.

