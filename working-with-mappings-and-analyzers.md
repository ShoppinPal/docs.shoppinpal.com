## Mappings and Analyzers

### Mappings:

Mappings are the process of defining how a document should be mapped in elasticsearch. i.e. How the data should be interpreted.

Each type in elasticsearch has a mapping.

To Retrieve the existing mapping for a given type, you can use:

```
GET /{index-name}/{type}/_mapping
```

For Identifaction, Elasticsearch has following Data Types:

1. Numeric Types          =&gt;  Byte,Short,Integer & Long
2. Floating Point Types =&gt;  Float,Double
3. Date
4. Boolean
5. Objects
6. String

There is also an implicit ` _all `field which is the concatenation of all the fields inside a document.

Different mapping for type can return different search results.

Custom mappings are possible.

#### For Defining Custom Mapping For Type:

```
PUT /bnext
{
  "mappings": {
    "sharing" : {
        "properties": {
           "pid":{
             "type": "string",
             "index":"not_analyzed"   # this code specifies that 
                                      # particular field should not be analyzed 
                                      # during index creation therefore will not be searched. 
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

**Note**:  Custom mappings can only be specified during index creation, once indexed mappings cannot be modified as there may be data in index belonging to that mapping. Kamal has recently done a chapter about **Re-Indexing**. \(worth a read\).



#### Analysis:

There are two types of searches in elasticsearch.

1. Exact Value Match
2. Full-Text Search

##### **1.Exact Value Match:**

In this search, fields are search for exact value match i.e. Searching all records where book name == "John Doe".

##### 2.Full Text Search:

In this search, ES searches for partial match based on specified keywords. i.e. find all books where discription has words "Hunger","adventure" and "Fantacy".



For Utilizing these searches to their fullest, analysis needs to be performed.Analysis can be summarized to specifying:

* Abbreviations
* Stemming     
* Typo Handling

We will be looking at each of them now.

#####  1. Abbreviations:

    Using analyzers, we can tell elasticsearch how to treat abbreviations in our data i.e. dr =&gt; Doctor so whenever we search for doctor keyword in our index, elasticsearch will also return the results which have dr mentioned in them.

#####  2. Stemming:

    Using stemming in analyzers allows us to use base words for modified verbs like  

| Words | Modifications |
| :---: | :---: |
| require | requirements,required |

#####  3. Typo Handling:

       Analyzers also provide typo handling as while querying if we are searching for particular word say 'resurrection', then elasticsearch will return the results in which typos are present.i.e. it will treat typos like resurection,ressurection as same and will retun the result. 

| Words | Modifications |
| :---: | :---: |
| resurrection | resurection,ressurection |



### Analyzers in Elasticsearch

 1. Standard

 2. Simple

 3. Whitespace

 4. Stop

 5. Keyword

 6. Pattern

 7. Language

 8. Snowball













