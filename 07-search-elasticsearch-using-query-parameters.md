# [07. Search Elasticsearch Using Query Parameters](https://egghead.io/lessons/tools-search-elasticsearch-using-query-parameters)

We can use `_search` with query parameters to further limit our queries.

To find all documents that have 'Homer' in the title, we could do the following:
```bash
$ curl -s 'localhost:9200/_all/episode/_search?q=title:Homer'
```

To find all documents that have 'Homer' in the title from season 5, we could use the following command using [URL encoding](https://www.w3schools.com/tags/ref_urlencode.ASP):
```bash
$ curl -s 'localhost:9200/_all/episode/_search?q=%2Btitle%3AHomer+%2Bseason%3A5'
```

Which is equivant to: `q=+title:Homer++season:5`

To find all documents that have 'Homer' and 'Bart' in the title that also have an IMDB rating greater than 8, use the following command:
```bash
curl -s 'localhost:9200/_search?q=%2Btitle%3A%28Homer%2BBart%29+%2Bimdb_rating%3A%3E8'
```

Which is equivalent to: `q=+title:(Homer+Bart)++imdb_rating:>8`

### Resources 

[Query String Query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html)<br>
[HTML URL Encoding Reference](https://www.w3schools.com/tags/ref_urlencode.ASP)