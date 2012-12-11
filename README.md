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


## Create


#Contributors

* Thad Clay ([thadclay](https://github.com/thadclay))
* Jan Paul Erkelens ([jperkelens](https://github.com/jperkelens))
* Micah Silverman ([dogeared](https://github.com/dogeared))
* Rob Malko ([malkomalko](https://github.com/malkomalko))
* Jim Drannbauer ([excellentdrums](https://github.com/excellentdrums))
