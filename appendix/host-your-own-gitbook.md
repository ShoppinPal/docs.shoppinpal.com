# Host your own Gitbook

## Repositories

It is worth exploring these pre-existing repositories:

1. Prebuilt images based on a `Dockerfile`
   1. [https://github.com/billryan/docker-gitbook](https://github.com/billryan/docker-gitbook)
   2. [https://github.com/humangeo/gitbook-docker](https://github.com/humangeo/gitbook-docker)
2. CI for build triggers and Gitbook all packaged neatly via `docker-compose.yml`
   1. [https://github.com/corncandy/docker-cluster](https://github.com/corncandy/docker-cluster)
3. Others
   * [https://github.com/tobegit3hub/gitbook-server](https://github.com/tobegit3hub/gitbook-server)
   * [https://github.com/humangeo/gitbook-docker](https://github.com/humangeo/gitbook-docker)

## Quick Setup

### Without CI

1. Clone your pre-existing gitbook repo to your cloud-box

   ```text
   cd ~/dev
   git clone https://github.com/ShoppinPal/docs.shoppinpal.com
   cd ~/dev/docs.shoppinpal.com
   ```

2. Add the following `docker-compose.yml` file at the cloned repo's root folder:

   ```text
   version: '2'
   services:
     gitbook:
       container_name: training
       image: billryan/gitbook:latest
       ports:
         - "4000:4000"
       volumes:
         - ./:/gitbook
         - ./docker-entrypoint-gitbook.sh:/apps/docker-entrypoint-gitbook.sh
       entrypoint: /apps/docker-entrypoint-gitbook.sh
   ```

3. Add the following `docker-entrypoint-gitbook.sh` file at the cloned repo's root folder:

   ```text
   #!/bin/bash
   #gitbook init
   gitbook serve --log=debug --debug
   #gitbook build --log=debug --debug
   ```

4. Setup permissions: `chmod 744 docker-entrypoint.sh`
5. Run `docker-compose up` to start
6. Run `docker-compose stop` to stop
7. Run `docker-compose up --force-recreate` to rebuild and launch from scratch
8. Run `docker-compose down` to tear it all down and cleanup

### With CI

1. TODO - @harshadyeola can add it here ...

## Alternative Setup

1. Clone your gitbook repo
2. Use gitbook desktop editor to edit and save
3. Use cmd line to push changes

