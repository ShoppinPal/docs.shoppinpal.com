# Setup a machine in the cloud

## Setup box on Azure

1. Login to Azure. You can use a personal account or request access to your company account. Ask your company's devops team for a terraform script to accomplish this in minutes.
1. Optionally, we recommend that you map your `<machine-ip>` to a friendly domain name like `<myName-cloud-box-1.domain.com>`
    1. If you have a CloudFlare account, use it.
    1. **Configure cloudflare for DNS only. Bypass any HTTP related CDN.**
    1. This may take some time to take effect and will hopefully be ready for you to use by the time you finish rest of the steps.
1. Use `ssh` to login:
    1. either: `ssh <username>@<machine-ip>`
    1. or: `ssh <username>@<myName-cloud-box-1.domain.com>`
1. Install `docker-compose` on your cloud box. You can copy-paste the following script, which is a multi-line command and it will "just work."

    ```
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
1. At this point you have a powerful and scalable setup. We will put it to good use as we explore various exercises in this training guide.
1. Let's do a small exercise to show off the power of this setup.
1. Clone a sample github project and launch it:

    ```
mkdir -p ~/dev && cd ~/dev && \
git clone https://github.com/ShoppinPal/loopback-mongo-sandbox.git && \
cd ~/dev/loopback-mongo-sandbox && \
docker-compose run builder npm install && \
docker-compose up
    ```
1. What did we just do?
  1. Cloned a project.
  1. Installed dependencies.
  1. Finally the `docker-compose up` command:
      1. launched the app by mounting the local source code and dependencies into a docker container,
      2. and launched MongoDB as its database.
1. Troubleshooting
    1. If you run into this problem:
        ```
        Couldn't connect to Docker daemon at http+docker://localunixsocket - is it running?
        ```
        1. try adding your user to the `docker` group, [reference](https://github.com/docker/compose/issues/1214):
            * `sudo usermod -aG docker <username>`
        1. if that doesn't do it, then login/logout of the ssh session
        1. ultimately restart your machine and that should definitely do it.
1. Let's browse to `http://<machine-ip>:3000/explorer` to see a fully working REST~ful API!
    1. If you had setup a DNS record previously then you can also try: `http://<myName-cloud-box-1.domain.com>:3000/explorer` to see a fully working REST~ful API!
