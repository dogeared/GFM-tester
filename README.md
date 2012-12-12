[![Build Status](https://secure.travis-ci.org/didit-tech/FastLegS.png)](http://travis-ci.org/didit-tech/FastLegS)
#FastLegS

PostgreSQL ORM on top of node-postgres.

##Installation

    npm install FastLegS

## Quickstart

**NOTE:** As of version```0.2.0```, both PostgreSQL and MySQL are supported. You indicate which database you are using at object instantiation time. All other operations and interfaces behave the same as older versions.

### Setup for versions < ```0.2.0```

    var FastLegS = require('FastLegS');
    ...
    FastLegS.connect(connectionParams);
    ...

### Setup for versions >= ```0.2.0```   

### MySQL:

    var FastLegSBase = require('FastLegS');
    var FastLegS = new FastLegSBase('mysql');
    ...
    FastLegS.connect(connectionParams);
    ...

### PostgreSQL:

    var FastLegSBase = require('FastLegS');
    var FastLegS = new FastLegSBase('pg');
    ...
    FastLegS.connect(connectionParams);
    ...

### Example:

    var FastLegSBase = require('FastLegS');

    // gonna use PostgreSQL
    var FastLegS = new FastLegSBase('pg');

    var connectionParams = {
      user: 'shes'
    , password: 'got'
    , database: 'legs'
    , host: 'localhost'
    , port: 5432
    }

    FastLegS.connect(connectionParams);

    var Post = FastLegS.Base.extend({
      tableName: 'posts',
      primaryKey: 'id'
    });

    Post.create({ title: 'Some Title 1', body: 'Some body 1' }, function(err, results) {
      Post.find({ 'title.ilike': '%title%' }, { only: ['id', 'body'] }, function(err, post) {
        // Hooray!
      });
    });

#The Full Monty

The following examples use these database tables as examples:

### posts

| id   | title        | blurb        | body        | published   |
|------|--------------|--------------|-------------|-------------|
| 1    | Some Title 1 | Some blurb 1 | Some body 1 | false       |
| 2    | Some Title 1 | Some blurb 2 | Some body 2 | true        |
| 3    | Some Title 1 | Some blurb 3 | Some body 3 | false       |
| 4    | Some Title 1 | Some blurb 4 | Some body 4 | true        |

### comments

| id | post_id | comment   | created_at |
|----|---------|-----------|------------|
|  1 |       1 | Comment 1 | 2012-12-11 |
|  2 |       1 | Comment 2 | 2012-12-11 |
|  3 |       2 | Comment 3 | 2012-12-11 |
|  4 |       2 | Comment 4 | 2012-12-11 |
|  5 |       3 | Comment 5 | 2012-12-11 |
|  6 |       3 | Comment 6 | 2012-12-11 |
|  7 |       4 | Comment 7 | 2012-12-11 |
|  8 |       4 | Comment 8 | 2012-12-11 |

Given this setup:
    
    var FastLegSBase = require('FastLegS');
    
    // gonna use PostgreSQL
    var FastLegS = new FastLegSBase('pg');
    
    var connectionParams = { 
      user: 'shes', password: 'got', 
      database: 'legs', host: 'localhost', port: 5432
    }
    
    FastLegS.connect(connectionParams);

The following are examples of basic CRUD operations:

## Create

Create can take an object or an array of objects.

    Post.create({ id: 5, title: 'Some Title 5', body: 'Some body 5' }, function(err, results) {
    
    })
    
    Post.create(
      [{ id: 6, title: 'Some Title 6', body: 'Some body 6' },
       { id: 7, title: 'Some Title 7', body: 'Some body 7' }],
      function(err, results) {
    
      }
    )

#Contributors

* Thad Clay ([thadclay](https://github.com/thadclay))
* Jan Paul Erkelens ([jperkelens](https://github.com/jperkelens))
* Micah Silverman ([dogeared](https://github.com/dogeared))
* Rob Malko ([malkomalko](https://github.com/malkomalko))
* Jim Drannbauer ([excellentdrums](https://github.com/excellentdrums))
