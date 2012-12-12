[![Build Status](https://secure.travis-ci.org/didit-tech/FastLegS.png)](http://travis-ci.org/didit-tech/FastLegS)
#FastLegS

PostgreSQL ORM on top of node-postgres.

##Installation

    npm install FastLegS

##Quickstart

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
    
    var callback = function(err, results) {
      console.dir(err);
      console.dir(results);
    }

The following are examples of basic CRUD operations:

##Create

Calls to ```create``` can take an object or an array of objects.

    Post.create(
      { id: 5, title: 'Some Title 5', body: 'Some body 5' }, 
      callback
    )

    Post.create(
      [{ id: 6, title: 'Some Title 6', body: 'Some body 6' },
       { id: 7, title: 'Some Title 7', body: 'Some body 7' }],
      callback
    )

The ```results``` passed to the callback are different depending on the database. 

In the case of PostgreSQL, the ```results``` will be an object of the form:

    {
      rows: [{ id: 5,
             title: 'Some Title 5',
             blurb: null,
             body: 'Some body 5',
             published: null }],
      command: INSERT,
      rowCount: 1,
      oid: 0
    }

In the case of MySQL, the ```results``` will be an object of the form:

    { 
      fieldCount: 0,
      affectedRows: 1,
      insertId: 0,
      serverStatus: 2,
      warningCount: 0,
      message: '' 
    }

##Read

The various forms of the ```find``` command are very flexible. We'll present a few of them here.

####By primary key

find:

    Post.find(6, callback)

returns:

    { 
      id: 6,
      title: 'Some Title 6',
      blurb: null,
      body: 'Some body 6',
      published: null,
      created_at: null,
      updated_at: null 
    }
    
find:

    Post.find(6, {only: ['id','title']}, callback)

returns:

    { id: 6, title: 'Some Title 6' }

##ToDo

Watch for updates to examples in the near future to show features like relationships and advanced queries.