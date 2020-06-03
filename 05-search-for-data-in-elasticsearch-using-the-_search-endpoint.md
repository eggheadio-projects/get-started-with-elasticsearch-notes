# [04. Search for Data in Elasticsearch Using the `_search` Endpoint](https://egghead.io/lessons/tools-search-for-data-in-elasticsearch-using-the-_search-endpoint)

The Elasticsearch `_search` API endpoint allows one to execute a search query and receive search hits that match the query as the result.
```bash
$ curl -s localhost:9200/_search
```

## Breaking Down the `_search` Response

+ `"took"` refers to the amount of time that passed (in milliseconds) while the search was being performed.

+ `"_shards"` includes the `"total"` number of shards that were involved as well as how many were  `"successful"` and how many `"failed"`.

+ `_search` has `"timed_out"` set to false as a default which means that Elasticsearch is going to run however long it takes to return the results. 

  + You can specify the amount of time that is desired to wait before receiving the results if needed, however `"timed_out"` doesn't stop the query from running. It continues to run in the background until it is complete. 

+ The desired data from our search can be found within an array called `"hits"`. Within this array we have the `"total"` number of documents as well as multiple of the documents themselves.

  + By default, the `_search` query returns 10 documents.

+ Within each document there is a `"_score"` field which refers to it's score in relation to how well the document matches the query. 

  + By default, the documents with the highest relevancy `"_score"` are listed first.  

## Refining `_search`

We can refine our search by specifying an `"_index"`.
```bash
$ curl -s localhost:9200/simpsons/_search
```

We can add multiple indices by adding a comma.
```bash
$ curl -s localhost:9200/simpsons,egghead/_search
```

We can also make use of the [wildcard](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-wildcard-query.html) operator to get any `"_index"` starting with a letter.
```bash
$ curl -s 'localhost:9200/s*,e*/_search'
```

We can continue to refine our search by adding more parameters such as the `"_type"`. 

### Resources

[Search API](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-search.html)<br>
[Wildcard Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-wildcard-query.html)
