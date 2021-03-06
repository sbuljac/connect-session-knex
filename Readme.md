# Connect Session Knex

connect-session-knex is a session store using [knex.js](http://knexjs.org/), which is a SQL query builder for Postgres, MySQL, MariaDB and SQLite3. Note: I could not get it to work with MariaDB using the mysql or mariadb drivers, but in general you're better off using PostgreSQL than MySQL.

## Installation

	  $ npm install connect-session-knex

## Options

 - `tablename='sessions'` Tablename to use. Defaults to 'sessions'.
 - `knex` knex instance to use. Defaults to a new knex instance, using sqlite3 with a file named 'connect-session-knex.sqlite'

## Usage

  With express 4.x:
  
    var session = require('express-session');
    var KnexSessionStore = require('connect-session-knex')(session);

    app.use(express.session({
      store: new KnexSessionStore,
      secret: 'your secret',
      cookie: { maxAge: 7 * 24 * 60 * 60 * 1000 } // 1 week
    }));
    
  With express 3.x:
  
    var KnexSessionStore = require('connect-session-knex')(express);

    app.configure(function() {
      app.use(express.session({
        store: new KnexSessionStore,
        secret: 'your secret',
        cookie: { maxAge: 7 * 24 * 60 * 60 * 1000 } // 1 week
      }));
    });
    
  With connect:

    var connect = require('connect'),
        KnexSessionStore = require('connect-session-knex')(connect);

    connect.createServer(
      connect.cookieParser(),
      connect.session({ store: new KnexSessionStore, secret: 'your secret' })
    );

    
## Benchmarks

https://github.com/llambda/express-session-benchmarks
