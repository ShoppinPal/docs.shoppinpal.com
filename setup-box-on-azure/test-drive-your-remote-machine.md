# Setup a machine in the cloud

## Test drive your remote machine

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
    2. If all the containers are up and you are still not able to access the application from browser, then make sure you have enabled inbound/outbound security rules on your remote host.
