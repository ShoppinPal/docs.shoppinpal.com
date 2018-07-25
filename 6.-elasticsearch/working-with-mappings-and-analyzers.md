# Working with Mappings and Analyzers

## Mappings:

Mappings are the process of defining how a document should be mapped in elasticsearch. i.e. How the data should be interpreted.

Each type in elasticsearch has a mapping.

To Retrieve the existing mapping for a given type, you can use:

```text
GET /{index-name}/{type}/_mapping
```

For identification, Elasticsearch has following Data Types:

1. Numeric Types          =&gt;  Byte,Short,Integer & Long
2. Floating Point Types =&gt;  Float,Double
3. Date
4. Boolean
5. Objects
6. String

There is also an implicit `_all`field which is the concatenation of all the fields inside a document.

Different mapping for type can return different search results.

Custom mappings are possible.

### For Defining Custom Mapping For Type:

```text
PUT /yourIndexName
{
  "mappings": {
    "sharing" : {
        "properties": {
           "pid":{
             "type": "string",
             "index":"not_analyzed"   # this code specifies that 
                                      # particular field should not be analyzed 
                                      # during index creation therefore will be matched as exact value. 
           },
           "shared_by":{
             "type": "string"
           },
           "shared_with":{
             "type": "string"
           },
           "path":{
              "type":"string",
              "analyzer":"english"   # this code will specify that this field 
                                     # should be analyzed using english analyzer.
          }
      }
    }
  }
}
```

**Note**: Custom mappings can only be specified during index creation. Once indexed, mappings cannot be modified as there may be data in index belonging to that mapping. Kamal has recently done a chapter about **Re-Indexing**. \(worth a read\).

There are two types of searches in elasticsearch.

1. Exact Value Match
2. Full-Text Search

#### **1.Exact Value Match:**

In this search, fields are search for exact value match i.e. Searching all records where book name == "John Doe".

#### 2.Full Text Search:

In this search, ES searches for partial match based on specified keywords. i.e. find all books where discription has words "Hunger","adventure" and "Fantasy".

## Analysis:

For Utilizing these searches to their fullest, analysis needs to be performed. Analysis can be summarized to specifying:

* Abbreviations
* Stemming
* Typo Handling

We will be looking at each of them now.

#### 1. Abbreviations:

Using analyzers, we can tell elasticsearch how to treat abbreviations in our data i.e. `dr = Doctor`. So whenever we search for `doctor` keyword in our index, elasticsearch will also return the results which have `dr` mentioned in them.

#### 2. Stemming:

Using stemming in analyzers allows us to use base words for modified verbs like

| Words | Modifications |
| :---: | :---: |
| require | requirements,required,requires,requiring |

#### 3. Typo Handling:

Analyzers also provide typo handling as while querying if we are searching for particular word say `resurrection`, then elasticsearch will return the results in which typos are present.i.e. it will treat typos like `resurection,ressurection` as same and will return the result.

| Words | Modifications |
| :---: | :---: |
| resurrection | resurection,ressurection |

## Analysis Phases:

* **Tidy Up The Body**
  * Analysis involves removing irrelevant stuff like applying character filters e.g. removing html tags
* **Tokenize the Body**
  * Tokenizers:
    * tokenizers can be used to remove whitespaces and generate tokens.
* **Normalization of Tokens**
  * After token generation, we need to normalize these tokens. for eg. lowercase all tokens.

## [Analyzers](https://www.elastic.co/guide/en/elasticsearch/reference/2.4/analysis-analyzers.html) in Elasticsearch:

There are few in-built analyzers in elasticsearch.

1. Standard
2. Simple
3. Whitespace
4. Stop
5. Keyword
6. Pattern
7. Language
8. Snowball

Though we can configure our own custom analyzers too. We will be configuring Path Analyzer in this tutorial.

In the following query, I am indexing an index named 'elastic\_course' and type 'Book' where analyzers and custom mappings are defined.

```text
PUT /elastic_course
{
  "settings": {
    "analysis": {
      "analyzer": {
        "path_analyzer": {
          "tokenizer": "path_tokenizer"
        }
      },
      "tokenizer": {
        "path_tokenizer": {
          "type": "path_hierarchy",  # Tokenizer Type
          "delimiter": "/",          # this specifies the character which will be 
                                     # used to split the body and generate tokens.   
          "replacement": "-"         # this field will be an alternative for delimiter.
        }
      }
    }
  },
  "mappings": {
    "book" : {
        "properties": {
           "author": {
              "type": "string",
              "index": "not_analyzed"  # will be matched as exact value
           },
           "genre": {
              "type": "string",
              "index": "no"            # will be skipped while searching.
           },
           "score": {
              "type": "double"
           },
           "synopsis": {
              "type": "string",
              "index":"analyzed",
              "analyzer":"english"     # here we are using built-in analyzers.
           },
           "title": {
              "type": "string"
           },
           "path":{
              "type":"string",
              "analyzer":"path_analyzer"  # here we are specifying that our custom analyzer 
                                          # will be used on this field.
          }
      }
    }
  }
}
```

