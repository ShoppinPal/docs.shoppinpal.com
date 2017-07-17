# Setup a machine in the cloud

## Setup box

_**Note**: Even without the video, you can learn all the crucial details from the steps that are documented below_

{% youtube %}https://youtu.be/sY9o3TbkXVc{% endyoutube %}

1. Login to DigitalOcean. You can use a personal account or request access to your company account.
2. Provision a machine with docker pre-installed.
3. Optionally, we recommend that you map your `<machine-ip>` to a friendly domain name like `<myName-cloud-box-1.domain.com>`
    1. If you have a CloudFlare account, use it.
    1. Configure cloudflare for DNS only. Bypass any HTTP related CDN.
    1. This may take some time to take effect and will hopefully be ready for you to use by the time you finish rest of the steps.
4. Use `ssh` to login: `ssh root@<machine-ip>`
5. Install `docker-compose` on your cloud box. You can copy-paste the following script, which is a multi-line command and it will "just work."

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
  curl -sSI https://github.com/docker/compose/releases/latest |
    tr -d '\r' |
    awk -F'/' '/^Location:/{print $NF}'
) && \
curl -L "https://github.com/docker/compose/releases/download/${LATEST}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
chmod +x /usr/local/bin/docker-compose && \
docker-compose --version
    ```
6. Install `nvm` to manage NodeJS

    ```
sudo apt-get --assume-yes install build-essential libssl-dev && \
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh -o install_nvm.sh && \
bash install_nvm.sh && \
source ~/.profile && \
nvm install 0.10
    ```
7. At this point you have a powerful and scalable setup. We will put it to good use as we explore various exercises in this training guide.
8. Let's do a small exercise to show off the power of this setup.
9. Clone a sample github project and launch it:

    ```
mkdir -p ~/dev && cd ~/dev && \
git clone https://github.com/ShoppinPal/loopback-mongo-sandbox.git && \
cd ~/dev/loopback-mongo-sandbox && \
npm install && \
docker-compose up
    ```
10. What did we just do?
  1. Cloned a project.
  1. Installed dependencies.
  1. Finally the `docker-compose up` command:
      1. launched the app by mounting the local source code and dependencies into a docker container,
      2. and launched MongoDB as its database.
11. Let's browse to `http://<machine-ip>:3000/explorer` to see a fully working REST~ful API!
    1. If you had setup a DNS record previously then you can also try: `http://<myName-cloud-box-1.domain.com>:3000/explorer` to see a fully working REST~ful API!
