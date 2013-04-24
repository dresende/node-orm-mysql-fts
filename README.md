## ORM MySQL Full-Text Search Plugin [![](https://badge.fury.io/js/orm-mysql-fts.png)](https://npmjs.org/package/orm-mysql-fts)

This plugin adds FTS support for the MySQL driver of [ORM](http://github.com/dresende/node-orm2).

## Dependencies

Of course you need `orm` to use it. Other than that, no more dependencies.

## Install

```sh
npm install orm-mysql-fts
```

## DBMS Support

- MySQL

## Usage

```js
Model.match(property1, property2, ...).against(expression [ , alias ])
```

`alias` is an alias for the `MATCH (..) AGAINST (..)` expression and by default is `"score"`. By default the query will
be ordered descending by this alias. Only matched rows will be returned (`HAVING score > 0`).

## Example

```js
var orm = require("orm");
var fts = require("orm-mysql-fts");

orm.connect("mysql://username:password@host/database", function (err, db) {
	if (err) throw err;

	db.use(fts);

	var Person = db.define("person", {
		name      : String,
		surname   : String,
		age       : Number
	});

	Person.match("name").against("john").limit(10).run(function (err, people) {
		// .against() returns a ChainFind, you can use .limit() , .where() ..
		// (by default it orders by best match)
	});
});
```
