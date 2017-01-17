# Setup a machine in the cloud

## What is the problem?

I work remotely so when I was presented with an opportunity to travel and work side-by-side with my team, I was quite excited. But just a day before my travel plans, I received an update from `Docker for Mac beta` that made it impossible for me to download any container images due to some `ipv6` issues. After reaching my destination, the bandwidth became a challenge and I also learned that my immediate team found it extremely wasteful to use docker and docker-compose for the same reason. This coupled with the need for slightly more powerful machines \(bigger solid-state-drive `SSD`\), was why docker adoption across our company had been slow! We were well into adopting docker into staging and production but we would always trip over simple issues. It took days to get a solution from developer's environment to the staging environment.

## What is the solution?

We decided to resolve the bandwidth issue by hosting private machines in the cloud. Naturally, any container image downloads would be much faster for a machine sitting inside a datacenter. And the only stress on our bandwidth would be for the `ssh` session to the cloud-box which was minimal. Large and quickly scrolling logs could be problematic but they were manageable. Using solutions like `screen` or `mosh` further eased any concerns about `ssh` hang-ups which could kill our running containers.

![](/assets/box_in_cloud_3.jpeg)

## Setup

1. Login to DigitalOcean. You can use a personal account or request access to your company account.
2. Provision a machine with docker pre-installed.
3. Optionally, we recommend that you map your `<machine-ip>` to a friendly domain name. If you have a CloudFlare account, use it.
4. Use `ssh` to login: `ssh root@<machine-ip>`
5. Install `docker-compose` on your cloud box. You can copy-paste the following script, which is a multi-line command and it will "just work."

    ```
sudo apt-get update && \
sudo apt-get install apt-transport-https ca-certificates && \
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D  && \
echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list && \
sudo apt-get update && \
sudo apt-get install mosh && \
sudo apt-get install docker-engine && \
sudo service docker start && \
curl -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
chmod +x /usr/local/bin/docker-compose && \
docker-compose --version
    ```
6. At this point you have a powerful and scalable setup. We will put it to good use as we explore various exercises in this training guide.

## Challenges

Configuring the cloud-box per person is still a manual activity! We hope to cut this down to minutes with terraform scripting one day.

Some IDEs did a [poor job](../bug-in-webstorm-deployments.html) of syncing developer's local code to the cloud-box so we setup a recurring rsync which had a one-time setup cost.

## How was it received?

When we presented this solution to our developers who had struggled with adopting docker in the past, we received positive feedback. On our first day of adoption, we even discovered and resolved what would have become a `dev-to-staging` issue. It was bound to crop up late in the cycle and cause a crisis amongst developers and devops regarding product-readiness and now they found themselves working alongside to tackle issues quickly without any negative perceptions.

### Author TODOs:

- record a 5 min video where you get a digitalocean machine and set it up
- record a 2 min video where you use a script to set it up
- share the gist for the script for publication
etc.