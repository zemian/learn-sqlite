Home: https://www.sqlite.org/index.html

CLI: https://www.sqlite.org/cli.html

DataTypes: https://www.sqlite.org/datatype3.html

## Create New Database

SQLite is really light! There is no server process needed to run. To create a new database, you just give a file name. If file exists, it will use it as existing database!

    sqlite3 test.db

NOTE: You will not see this file unless you start write to it.

You can also start a in-memory DB without a file parameter.

## Quick Client (Dot) Commands

```
.databases
.tables
.schema hello
.quit
```

See https://sqlite.org/cli.html

NOTE: If you make a mistake on the command line, just end it with `;` to let it failed, then retry.

## Quick SQL Test

```sql
create table hello(name text, num int);
insert into hello values('foo', 123);
insert into hello values('foo2', 123);
select * from hello;
update hello set num = 99 where name = 'foo';
delete from hello where name = 'foo';
```

## Load SQL from File

    sqlite> .read examples/test.sql

## Sample DB

An online music store DB: chinook.db 

https://www.sqlitetutorial.net/sqlite-sample-database/

## DataTypes

NOTE: The datatype is optional in SQLite!

SQLite is very flexible with regard to datatypes.

Some commentators say that SQLite is "weakly typed" and that other SQL databases are "strongly typed". We consider these terms to be inaccurate and pejorative. We prefer to say that SQLite is "flexibly typed" and that other SQL databases are "rigidly typed".

Each value stored in an SQLite database (or manipulated by the database engine) has one of the following storage classes:

```
NULL. The value is a NULL value.

INTEGER. The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.

REAL. The value is a floating point value, stored as an 8-byte IEEE floating point number.

TEXT. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).

BLOB. The value is a blob of data, stored exactly as it was input.
```

See also on "Type Affinity" - The preferred storage class for a column is called its "affinity".

Each column in an SQLite 3 database is assigned one of the following type affinities:

TEXT
NUMERIC
INTEGER
REAL
BLOB

* A column with TEXT affinity stores all data using storage classes NULL, TEXT or BLOB.
* A column with NUMERIC affinity may contain values using all five storage classes. 
* A column that uses INTEGER affinity behaves the same as a column with NUMERIC affinity. 
* A column with REAL affinity behaves like a column with NUMERIC affinity except that it forces integer values into floating point representation.
* A column with affinity BLOB does not prefer one storage class over another and no attempt is made to coerce data from one storage class into another.

## DateTime Type and Functions

SQLite has no DATETIME datatype. Instead, dates and times can be stored in any of these ways:

As a TEXT string in the ISO-8601 format. Example: '2018-04-02 12:13:46'.
As an INTEGER number of seconds since 1970 (also known as "unix time").
As a REAL value that is the fractional Julian day number.
The built-in date and time functions of SQLite understand date/times in all of the formats above, and can freely change between them. Which format you use, is entirely up to your application.

https://www.sqlite.org/lang_datefunc.html

```
SELECT date('now');
SELECT datetime(1092941466, 'unixepoch', 'localtime');
SELECT date('now','start of month','+1 month','-1 day');
SELECT strftime('%s','now');
SELECT strftime('%s','now') - strftime('%s','2004-01-01 02:34:56');
```

## To AUTOINCREMENT or Not TO?

https://www.sqlite.org/autoinc.html

The AUTOINCREMENT keyword imposes extra CPU, memory, disk space, and disk I/O overhead and should be avoided if not strictly needed. It is usually not needed.

In SQLite, a column with type INTEGER PRIMARY KEY is an alias for the ROWID (except in WITHOUT ROWID tables) which is always a 64-bit signed integer.

```
CREATE TABLE test1(a INT, b TEXT);
INSERT INTO test1(rowid, a, b) VALUES(123, 5, 'hello');
INSERT INTO test1(a, b) VALUES(5, 'hello');
SELECT *, ROWID from test1;
```
