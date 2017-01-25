# ElasticSearch

## Version Tools

[esvm](https://www.npmjs.com/package/esvm) - Elasticsearch Version Manager is a command line application used for development to manage different versions of Elasticsearch. Like `nvm` is for NodeJS, similarly `esvm` is for ElasticSearch.

## Useful plugins

### Curated
* [ES Head](https://github.com/mobz/elasticsearch-head) - simplest admin console for ES.
* [ES Inquisitor](https://github.com/polyfractal/elasticsearch-inquisitor) helps you understand:
    * how ES breaks down your text into tokens for storage, and
    * your search into tokens for lookups.
    * Access it at: `<proto>//<host>:<port>/_plugin/inquisitor/#/analyzers`
* [Sense](https://www.elastic.co/blog/found-sense-a-cool-json-aware-interface-to-elasticsearch) - An extension for the Chrome Browser. Very useful, you can find it in the chrome web store.

### Hear-Say
* [ES GUI](https://github.com/jettro/elasticsearch-gui) - An angularJS client for elasticsearch as a plugin.
* [Sensitive](https://github.com/gillyb/sensitive) - A native version of the `sense` plugin for elasticsearch
* [ReclineJS](http://reclinejs.com/) - for building good UI on top of `CouchDB`.
* [Approx](https://github.com/ptdavteam/elasticsearch-approx-plugin/) - to do approximate or exact distinct counts, and fast term lists
* [Elastic Facets](https://github.com/bleskes/elasticfacets) - A set of facets and related tools for ElasticSearch.
* [Elastic Hammer](https://github.com/andrewvc/elastic-hammer) - `Sense` would suffice in our opinion. The only additional merit we see, is that it renders images inline, when presenting search results.


`TODO for Authors:` Need to create a docker-compose file with an entrypoint script that installs this plugin for readers to play around with the most appropriate version of ES. Plugins usually can't keep up with the lightning fast progress of ES.

## Useful tips

### Analyzers
* It is possible to [define new analyzers](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/indices-update-settings.html#update-settings-analysis) for an index. But it is required to **close** the index first and **open** it after the changes are made.
* Gram-based approach:
    * http://jontai.me/blog/2013/02/adding-autocomplete-to-an-elasticsearch-search-application/
    * http://exploringelasticsearch.com/searching_usernames_and_tokenish_text.html#ch-strangetext
        * ngrams don’t attempt language heuristics such as stemming that don’t apply to strings like “cmdrtaco”. They also handle mis-spelled terms well, since a search just needs to have a plurality of matches of sub-parts of a given term
        * ngrams allow developers to trade storage for CPU
    * https://www.found.no/foundation/fuzzy-search/
        * https://www.found.no/foundation/text-analysis-part-1/#using-ngrams-for-advanced-token-searches
        * https://www.found.no/foundation/text-analysis-part-2/
* Autocomplete and various ways to get there:
  * http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-suggesters-completion.html
  * https://www.elastic.co/guide/en/elasticsearch/guide/master/_index_time_search_as_you_type.html

### Rebuilding an index
* Scan / [Scroll](http://www.elasticsearch.org/guide/en/elasticsearch/client/javascript-api/current/api-reference.html#api-scroll)
    * https://github.com/karussell/elasticsearch-reindex
        * cloned it
        * ran build:
            * mvn -DskipTests clean package
        * uploaded the zip from "target” directory to hosted ES
        * reindex operation errored out during trial & error
* [Word Delimiter](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-word-delimiter-tokenfilter.html)

## Examples & Exercises

`TODO for Authors:` Need to create a docker-compose file to setup and play with analyzers quickly.


`TODO for Authors:` Use `sense` chrome plugin or CURL to demonstrate.

```
GET /my_index/_analyze?field=product.image_url&text="t112_1059_Cinnamon - Incense Stick"

GET /_analyze?tokenizer=keyword&filters=lowercase&text="t112_1059_Cinnamon - Incense Stick"

GET /_analyze?token_filters=word_delimiter&text="O’Neil’s hello---there, dude SD500 PowerShot Wi-Fi"

GET /_analyze?tokenizer=standard&text="t112_1059_Cinnamon - Incense Stick"

GET /_analyze?analyzer=simple&text="t112_1059_Cinnamon - Incense Stick"

GET /_analyze?tokenizer=keyword&token_filters=word_delimiter,lowercase&text="t112_1059_Cinnamon - Incense Stick"

GET /my_index/_analyze?field=product.name&text="t112_1059_Cinnamon - Incense Stick"

POST /my_index/product/_search
{"query":{"bool":{"must":[{"query_string":{"default_field":"_all","query":"cinna"}}]}}}

POST /my_index/product/_search
{"query":{"bool":{"must":[{"query_string":{"default_field":"name","query":"cinnamon"}}]}}}

GET /my_index/_analyze?field=product.barcodes&text="['20015','20016']"

POST /my_index/product/_search
{
   "query": {
      "term": {
         "barcodes": "MANUAL:20015"
      }
   }
}
POST /my_index/product/_search
{
   "query": {
      "multi_match": {
         "query": "20015",
         "fields": [
            "barcodes"
         ]
      }
   }
}

POST /my_index/product/_search
{
   "query": {
      "match_all": {}
   },
   "facets": {
      "department_name": {
         "terms": {
            "field": "barcodes"
         }
      }
   }
}
```

