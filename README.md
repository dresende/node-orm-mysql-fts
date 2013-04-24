## ORM MySQL Full-Text Search Plugin

This plugin adds FTS support for the MySQL driver of []ORM.

## Dependencies

Of course you need `orm` to use it. Other than that, no more dependencies.

## Install

```sh
npm install orm-mysql-fts
```

## DBMS Support

- MySQL

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
