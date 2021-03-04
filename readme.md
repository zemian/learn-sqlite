https://www.sqlite.org/index.html

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
