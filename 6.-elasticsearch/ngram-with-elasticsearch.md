# NGram with Elasticsearch

## Setup a sandbox

_**Note**: Even without the video, you can learn all the crucial details from the steps that are documented below_

{% embed data="{\"url\":\"https://youtu.be/vinrUb8vab8\",\"type\":\"video\",\"title\":\"\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/vinrUb8vab8/maxresdefault.jpg\",\"width\":1280,\"height\":720,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/vinrUb8vab8?rel=0&showinfo=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/vinrUb8vab8?rel=0&amp;showinfo=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}

1. Login to your [cloud-box](https://github.com/shoppinpal/docs-shoppinpal-com/tree/8cdd099563d11c1fe1df4d584b504337850c59eb/setup-a-machine-in-the-cloud.html) over `ssh`
2. Create a directory for running an elasticsearch sandbox:

   ```text
   mkdir -p ~/dev/elasticsearch-sandbox
   ```

3. Step into the working directory:

   ```text
   cd ~/dev/elasticsearch-sandbox
   ```

4. Create a `docker-compose.yml` file to install and run elasticsearch:

   ```text
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

5. Create an entrypoint file named `docker-entrypoint-es2-plugins.sh` to install useful plugins:

   ```text
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

   ```text
   chmod 744 *.sh
   ```

7. Start the service: `docker-compose up`
8. Open a browser to view the two plugins running on ES:
   1. esHead - [http://your-cloud-box-ip:9202/\_plugin/head/](http://your-cloud-box-ip:9202/_plugin/head/)
   2. esInq - [http://your-cloud-box-ip:9202/\_plugin/elasticsearch-inquisitor/](http://your-cloud-box-ip:9202/_plugin/elasticsearch-inquisitor/)

## Play Around

1. Use the `Any Request` tab in `/_plugin/head/` to create an index with a custom analyzer for a 3 by 3 ngram:

   ```text
   PUT testing_ngram_3_by_3
   {
     "settings": {
       "analysis": {
         "analyzer": {
           "ngram_3_by_3": {
             "tokenizer": "ngram_3_by_3"
           }
         },
         "tokenizer": {
             "ngram_3_by_3": {
             "type": "ngram",
             "min_gram": 3,
             "max_gram": 3,
             "token_chars": [
               "letter",
               "digit"
             ]
           }
         }
       }
     }
   }
   ```

2. Go to `/_plugin/elasticsearch-inquisitor/#/analyzers` to see the `ngram_3_by_3` analyzer at the bottom of the page.
   * click the checkbox and then use the top most input field to see how the analyzer breaks down the input into tokens

     ![](../.gitbook/assets/ngram-inquisitor.png)

