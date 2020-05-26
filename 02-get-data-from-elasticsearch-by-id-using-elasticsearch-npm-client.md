# [02. Get Data From Elasticsearch by id Using the Elasticsearch npm Client](https://egghead.io/lessons/tools-get-data-from-elasticsearch-by-id-using-the-elasticsearch-npm-client)

## Installing the Elasticsearch npm Client

In order for your application to consume the Elasticsearch cluster data, we need to use the [Elasticsearch client](https://www.npmjs.com/package/elasticsearch) for Node.js which is maintained by the company who built Elasticsearch! To install this package, navigate to the terminal (which should already be in the project's directory) and use the command
```bash
$ npm install elasticsearch --save
```

*Quick side note: the `--save` flag saves the package to our `package.json` as a dependency.*

## Implementing the Elasticsearch npm Client

Now that we have the dependency installed, we need to create a `client.js` file within the top-level directory of the repository. Within this file we will need to require the dependency
```javascript
const ELASTICSEARCH = require("elasticsearch");
```

so that we can create a new client utilizing it.
```javascript
const CLIENT = new ELASTICSEARCH.Client({
  host: "localhost:9200",
  apiVersion: '7.6'
});
```

*Quick side note: we indicate the `apiVersion` here so that future updates won't negatively impact (i.e. break) the way our application functions.*

## Using the Elasticsearch npm Client

Now that we have created our Elasticsearch client we can use it! Let's perform a `HTTP GET` request on our newly created client by providing our desired parameters to the built in `get` method.
```javascript
CLIENT.get({
  index: "simpsons",
  type: "episode",
  id: 1
})
```

Before we run this file, we need to make sure that we add code to handle our response as well as catch any errors that may occur. 
```javascript
CLIENT.get({
  index: "simpsons",
  type: "episode",
  id: 1
}, function(err, resp) {
  if(err) {
    console.log(err);
  } else {
    console.log(resp);
  }
});
```

Now that we have our code written, let's run the file in the terminal using
```bash
$ node client.js
```

You'll notice that the response looks exactly the same as when we used the `curl` command in the first section. How neat is that? 

### Don't Like Callbacks?

If you aren't a fan of callbacks and would prefer to use promises instead, the client allows for that implementation as well.
```javascript
CLIENT.get({
    index: "simpsons",
    type: "episode",
    id: 1,
    _sourceIncludes: [
      'title'
    ]
  })
  .then(resp => {
    console.log(resp);
  })
  .catch(err => {
    console.error(err);
  });
```

*Quick side note: Will mentions that one could implement catching an error within the `.then` method, but it could lead to the error being "swallowed" if a bunch of promises are chained together.*

### Other `GET` Method Parameters

Now, similar to the `curl` command we used in section 01, we can implement other parameters in our `GET` request. We can utilize `_sourceExcludes` 
```javascript
CLIENT.get({
  index: "simpsons",
  type: "episode",
  id: 1,
  _sourceExcludes: [
    'image_url',
   ' number_in_season'
  ]
})
```

and `_sourceIncludes`
```javascript
CLIENT.get({
  index: "simpsons",
  type: "episode",
  id: 1,
  _sourceIncludes: [
    'title'
  ]
})
```

to receive the specific parameters that we want.