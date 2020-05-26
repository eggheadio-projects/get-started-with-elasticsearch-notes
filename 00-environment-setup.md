# 00. Environment Setup

In order to fully benefit from this course, it is recommended to use the course's GitHub repo. Make your way over to the [repository](https://github.com/rekibnikufesin/elasticsearch-intro) and fork it. Once that's completed, clone the repo onto your machine using `git clone [repo SSH key]`. 

## Prerequisites

Before jumping into this course, you should make sure that you have [Docker](https://docs.docker.com/) and [Elasticsearch](https://www.elastic.co/guide/index.html) downloaded on your local machine. You can click on the following links to download these tools.

+ [Docker Download Documentation](https://docs.docker.com/get-docker/)
+ [Elasticsearch Download Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/7.7/install-elasticsearch.html)

## Project Environment Setup

Once you have insured that you have Docker and Elasticsearch on your local machine, follow the "Setting Up" guidelines within the repository's README. Once you have successfully gotten the environment up and running, jump into the first video of the course!

## Having Environment Issues?

Don't worry, I also came across a few issues while setting up my local environment. Thankfully a few people have commented on how to fix the issues I delt with within the comments of the course's [first section](https://egghead.io/lessons/elasticsearch-get-data-from-elasticsearch-by-id-using-http).

Now let's jump into the issues I had in hopes that they'll help you.

### `utils/import.js`

I updated line 3 to 
```javascript
const csv = require('csvtojson/v1')
```

I also needed to update the `apiVersion` on line 12 to
```javascript
apiVersion: '7.6'
```

### `docker-compose.yml`

The version on line 1 needed to be updated to
```javascript
version: '3'
```