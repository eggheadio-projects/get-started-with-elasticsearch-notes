# [02. Get Data From Elasticsearch by id Using the Elasticsearch npm Client](https://egghead.io/lessons/tools-get-data-from-elasticsearch-by-id-using-the-elasticsearch-npm-client)

## Installing the Elasticsearch npm Client

In order for your application to consume the Elasticsearch cluster data, we need to use the [Elasticsearch client](https://www.npmjs.com/package/elasticsearch) for Node.js which is maintained by the company who built Elasticsearch! To install this package, navigate to the terminal (which should already be in the project's directory) and use the command
```bash
npm install elasticsearch --save
```

*Quick side note: the `--save` flag saves the package to our `package.json` as a dependency.*

## Implementing the Elasticsearch npm Client

