# [06. Paginate Through Search Results in Elasticsearch](https://egghead.io/lessons/tools-paginate-through-search-results-in-elasticsearch)

We can add `?size=` to our query to specify the number of results we'd like to receive.
```bash
$ curl -s 'localhost:9200/simpsons/episode/_search?size=5'
```

We can take it a step further and say we'd like to see the next five documents that match our query by adding `&from=5` to our query. 
```bash
$ curl -s 'localhost:9200/simpsons/episode/_search?size=5&from=5'
```

This allows us to paginate through the results, but it does have performance implications. This has to do with how Elasticsearch retreives and sorts search results. 

When you search, each shard generates its own top 10 results and those are sent to the coordinating node for a total of 50 results (I'm basing this off of our previous example of 5). As Will says in the video, "as you scale, the cost of sorting grows exponentially" which will impact performace. 

### Resources

[Search API](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-search.html#search-search-api-request-body)<br>
[Request Body Search](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-body.html)