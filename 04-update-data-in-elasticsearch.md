# [03. Update Data in Elasticsearch](https://egghead.io/lessons/tools-update-data-in-elasticsearch)

## Important Notes

+ Documents in Elasticsearch are immutable, they either need to be re-indexed or replaced. 

+ We cannot access the original version of a document once it has been overwritten/updated.

+ Arrays in Elasticsearch are not treated as objects like they are in JavaScript.

## How to Update a Document

We can use the `_update` API endpoint to make partial updates to our documents. 
```bash
$ curl -XPOST -H 'Content-type: application/json' -d '{"doc": {"views": 1001, "tags": ["elasticsearch"] }}' localhost:9200/egghead/lessons/3/_update
```

Within the above request, we specified an item called `"doc"` and inside of there is where we specify what fields we'd like to be updated/added. In our case we are updating the `"views"` field and adding a new field called `"tags"`. 

In order to know that our document has been updated, take a look at the `"result"` field within the response. It should say `"result": "updated"` if the update was successful. We can check the updated document itself by running 
```bash 
$ curl -s localhost:9200/egghead/lessons/3
```

We can use `"scripts"` to update a specific field instead of the whole document. 
```bash
$ curl -XPOST -H 'content-type: application/json' -d '{"script": "ctx._source.tags +=1" }' localhost:9200/egghead/lessons/3/_update
```

It is important to note that the above solution does have performance implications because it has to access `"_source"` so Will recommends sticking with updating the `"doc"`. 

## `_update` Deep Dive

The `_update` API endpoint 

+ gets the document from the index
+ merges our changes
+ writes the index back as a new version of that document

This all happens on the same [Elasticsearch shard](https://www.elastic.co/blog/how-many-shards-should-i-have-in-my-elasticsearch-cluster) with no network latency and it verifies if the verison number is still the same before commiting the change. If the version is no longer the same, it fails. If this happens, we can use the `retry_on_conflict` parameter which allows us to specify the number of times we'd like to retry. 
```bash
curl -XPOST -H 'content-type: application/json' -d '{"script": "ctx._source.views +=1" }' 'localhost:9200/egghead/lessons/3/_update?retry_on_conflict=5'
```

Will mentions that if it fails the number of times that has been specified that the issue should be escalated and addressed. 

### Resources

[Update API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update.html)<br>
[How many shards should I have in my Elasticsearch cluster?](https://www.elastic.co/blog/how-many-shards-should-i-have-in-my-elasticsearch-cluster)