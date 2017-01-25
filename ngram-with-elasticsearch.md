# NGram with Elasticsearch

## Setup a sandbox
1. Login to your [cloud-box](../setup-a-machine-in-the-cloud.html) over `ssh`
2. Create a directory for running an elasticsearch sandbox:
   ```
   mkdir -p ~/dev/elasticsearch-sandbox
   ```
3. Step into the working directory:
   ```
   cd ~/dev/elasticsearch-sandbox
   ```
4. Create a docker-compose.yml file to install and run elasticsearch:
   ```
   ## Version Selection for compose file
   # https://docs.docker.com/compose/compose-file/#/versioning
   version: '2'
   services:
   es_v2:
    image: elasticsearch:2
    ports:
     - "9202:9200"
    volumes:
     - ./docker-entrypoint-es2-plugins.sh:/apps/docker-entrypoint-es2-plugins.sh
    entrypoint: /apps/docker-entrypoint-es2-plugins.sh
   ```
56. Create an entrypoint file to install useful plugins:
   ```
   #!/bin/bash
   # setting up prerequisites

   # re-runs will give an error that is harmless:
   #   > ERROR: plugin directory /usr/share/elasticsearch/plugins/delete-by-query already exists.
   #   > To update the plugin, uninstall it first using 'remove delete-by-query' command
   #plugin install delete-by-query

   # https://github.com/mobz/elasticsearch-head/#running-as-a-plugin-of-elasticsearch
   plugin install mobz/elasticsearch-head

   # access it at /_plugin/elasticsearch-inquisitor/
   plugin install polyfractal/elasticsearch-inquisitor

   #exec /docker-entrypoint.sh elasticsearch
   exec elasticsearch -Des.insecure.allow.root=true
   ```

6. Make sure to change the permissions to execute `sh` files:
   ```
   chmod 744 *.sh
   ```
7. Start the service: `docker-compose up`
8. Open a browser to view the two plugins running on ES:
   1. http://<machine-ip>:9202/_plugin/head/
   2. http://<machine-ip>:9202/_plugin/elasticsearch-inquisitor/