---
layout: post
title: RESTful api with NodeJs and Postgres
category: 'technology'
---

Create a RESTful webservice with Javascript, Node, Express, Postgres, and pg-promise.

Tools and technologies:

-   Node.js
-   express
-   express-generator
-   Postgres
-   pg-promise
-   bluebird

##Project setup

Install the Express Generator:

    $ npm install express-generator -g

Create a new project and install the required dependencies:
    
    $ express node-postgres-promises
    $ cd node-postgres-promises
    $ npm install
    
Install pg-promise, simply, pg-promise abstracts away much of the difficult, low-level connection management, allowing you to focus on the business logic. Further, the library includes a powerful query formatting engine and support for **automated transactions**.
    
    npm install pg-promise --save
    
install Bluebird, it’s loaded with features and reputed to be faster than ES6 Promises.    


create a new file in the project root called queries.js:

    var promise = require('bluebird');
    
    var options = {
      // Initialization Options
      promiseLib: promise
    };
    
    var pgp = require('pg-promise')(options);
    var connectionString = 'postgres://localhost:5432/puppies';
    var db = pgp(connectionString);
    
    // add query functions
    
    module.exports = {
      getAllPuppies: getAllPuppies,
      getSinglePuppy: getSinglePuppy,
      createPuppy: createPuppy,
      updatePuppy: updatePuppy,
      removePuppy: removePuppy
    };
    
##Postgres setup
  
Create a new file also in the root called puppies.sql and then add the following code:

    DROP DATABASE IF EXISTS puppies;
    CREATE DATABASE puppies;
    
    \c puppies;
    
    CREATE TABLE pups (
      ID SERIAL PRIMARY KEY,
      name VARCHAR,
      breed VARCHAR,
      age INTEGER,
      sex VARCHAR
    );
    
    INSERT INTO pups (name, breed, age, sex)
      VALUES ('Tyler', 'Retrieved', 3, 'M');
      
Run the file to create the database, apply the schema, and add one row to the newly created database:
      
    $ psql -f puppies.sql
    
    DROP DATABASE
    CREATE DATABASE
    CREATE TABLE
    INSERT 0 1
    
##Routes
    
Now we can set up the route handlers in index.js:
    
    var express = require('express');
    var router = express.Router();
    
    var db = require('../queries');
    
    router.get('/api/puppies', db.getAllPuppies);
    router.get('/api/puppies/:id', db.getSinglePuppy);
    router.post('/api/puppies', db.createPuppy);
    router.put('/api/puppies/:id', db.updatePuppy);
    router.delete('/api/puppies/:id', db.removePuppy);
    
    module.exports = router;
    
##Queries
    
Next, let’s add the SQL queries to the queries.js file.

###GET All Puppies    

    function getAllPuppies(req, res, next) {
      db.any('select * from pups')
        .then(function (data) {
          res.status(200)
            .json({
              status: 'success',
              data: data,
              message: 'Retrieved ALL puppies'
            });
        })
        .catch(function (err) {
          return next(err);
        });
    }
    
###GET Single Puppy
    
    function getSinglePuppy(req, res, next) {
      var pupID = parseInt(req.params.id);
      db.one('select * from pups where id = $1', pupID)
        .then(function (data) {
          res.status(200)
            .json({
              status: 'success',
              data: data,
              message: 'Retrieved ONE puppy'
            });
        })
        .catch(function (err) {
          return next(err);
        });
    }
    
    $ curl http://127.0.0.1:3000/api/puppies/1
    
###POST
    
    function createPuppy(req, res, next) {
      req.body.age = parseInt(req.body.age);
      db.none('insert into pups(name, breed, age, sex)' +
          'values(${name}, ${breed}, ${age}, ${sex})',
        req.body)
        .then(function () {
          res.status(200)
            .json({
              status: 'success',
              message: 'Inserted one puppy'
            });
        })
        .catch(function (err) {
          return next(err);
        });
    }
    
    $ curl --data "name=Whisky&breed=annoying&age=3&sex=f" \
    http://127.0.0.1:3000/api/puppies
    
###PUT
    
    function updatePuppy(req, res, next) {
      db.none('update pups set name=$1, breed=$2, age=$3, sex=$4 where id=$5',
        [req.body.name, req.body.breed, parseInt(req.body.age),
          req.body.sex, parseInt(req.params.id)])
        .then(function () {
          res.status(200)
            .json({
              status: 'success',
              message: 'Updated puppy'
            });
        })
        .catch(function (err) {
          return next(err);
        });
    }
    
    $ curl -X PUT --data "name=Hunter&breed=annoying&age=33&sex=m" \
    http://127.0.0.1:3000/api/puppies/1
    
    
###Delete
    
    function removePuppy(req, res, next) {
      var pupID = parseInt(req.params.id);
      db.result('delete from pups where id = $1', pupID)
        .then(function (result) {
          /* jshint ignore:start */
          res.status(200)
            .json({
              status: 'success',
              message: `Removed ${result.rowCount} puppy`
            });
          /* jshint ignore:end */
        })
        .catch(function (err) {
          return next(err);
        });
    }
    
    $ curl -X DELETE http://127.0.0.1:3000/api/puppies/1
    
##Error Handling
    
    // development error handler
    // will print stacktrace
    if (app.get('env') === 'development') {
      app.use(function(err, req, res, next) {
        res.status( err.code || 500 )
        .json({
          status: 'error',
          message: err
        });
      });
    }
    
    // production error handler
    // no stacktraces leaked to user
    app.use(function(err, req, res, next) {
      res.status(err.status || 500)
      .json({
        status: 'error',
        message: err.message
      });
    });
    
##Questions
    
1, How to do authentication work for this code in real project?
    
http://passportjs.org/

2, How to refactor this code to separate routing logic from "controller" logic?

3, How to properly setup this for production in a scalable way(nginx, apache)?


    
    