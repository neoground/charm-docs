---
key:     core.database
title:   Database
section: Core Modules
nav:
  prev:
    page: core.confdebug
    icon: prev
    name: Config & Debug
  next:
    page: core.events
    icon: next
    name: Events
---

# ->>  Database & Redis <<-

<div class="card card-body" markdown="1">
Amidst the digital realm, the Database module emerges as the keeper of the sacred data, 
a realm where information is curated and stored in structured sanctuaries. 
In the journey through code, a developer seeks the knowledge ensconced within
these database halls, and with C::Database()->... as the key, the gateways to
these knowledge realms are unlocked. The module stands as a bridge, where structured 
queries turn into a stream of knowledge flowing into the application's veins. It's not
merely a module but a conjurer, casting spells of SQL to commune with the data deities 
enshrined within your database.

Database actions are mostly handled by the popular [Eloquent ORM](https://laravel.com/docs/10.x/database)
by Laravel.

Supported databases:

- MariaDB 10.10+
- MySQL 5.7+
- PostgreSQL 11.0+
- SQLite 3.8.8+
- SQL Server 2017+
</div>

## ->> Methodology

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/database1.jpg" alt="Section header image" /></div>

### -> Unveiling the Database Connection:
`getDatabaseConnection()`

With this invocation, the Eloquent instance is revealed, unlocking the full arsenal of features. For instance:
```php
C::Database()->getDatabaseConnection()->select('SHOW DATABASES');
```

### -> Discovering the Databases:
`getAllDatabases()`

Embark on a quest to unveil all the databases dwelling within your realm:
```php
$all_databases = C::Database()->getAllDatabases();
```

### -> Uncovering the Tables:
`getAllTables()`

Seek the tables harbored within your database realms:
```php
$all_tables = C::Database()->getAllTables();
```

### -> Revealing the Table Structure:
`getTableStructure(string $table_name)`

Delve deeper to understand the anatomy of a table:
```php
$table_structure = C::Database()->getTableStructure('heroes');
```

### -> ORM - The Chariot of Interaction:
The charm of ORM (Object-Relational Mapping) simplifies the voyage through the data realms, 
where models act as the chariots, ferrying developers across the river of queries.

</div>

## ->> Configuring The Database Connection

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/database2.jpg" alt="Section header image" /></div>

### Single Database:
The `connections.yaml` is the scroll where the details of your database realm are inscribed. 
Here’s a glimpse into the configuration for a single database:

```yaml
# SQL Database
# ---------------------------------------------
database:
  # Should the database connection be enabled?
  enabled:   true
  # Type of database
  driver:    mysql
  # Authentication
  host:      'localhost'
  username:  'dukenukem'
  password:  'LAm3ltd0wn!'
  # Database
  database:  'DatabaseName'
  prefix:    dn_
  charset:   utf8mb4
  collation: utf8mb4_unicode_ci
```

### Multiple Databases:
For those seeking to converse with multiple data realms, a slight alteration 
in the `connections.yaml` scroll unveils the path:

```yaml
# SQL Databases
# ---------------------------------------------
databases:
  default:
    enabled:   true
    driver:    mysql
    host:      'localhost'
    username:  'dukenukem'
    password:  'LAm3ltd0wn!'
    database:  'DatabaseName'
    prefix:    dn_
    charset:   utf8mb4
    collation: utf8mb4_unicode_ci
  otherstuff:
    enabled:   true
    driver:    mysql
    host:      'localhost'
    username:  'dukenukem'
    password:  'LAm3ltd0wn!'
    database:  'OtherStuffDatabase'
    prefix:    osdb_
    charset:   utf8mb4
    collation: utf8mb4_unicode_ci
```

Make sure you provide a default connection!

If you use multiple databases, one connection must always have the name `default`.

</div>

## ->> Database Dumping

<div class="card card-body" markdown="1">

A ritual to encapsulate the essence of your database into a dump, 
preserving it for the epochs to come. Invoke the `createDump()` method to commence the ritual:

```php
C::Database()->createDump('default')
             ->excludeTables(['foo', 'bar'])
             ->dumpToFile(PathFinder::getDataPath() . DS . 'dump.sql');
```

</div>

## ->> Redis: The Swift Messenger of Data

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/database3.jpg" alt="Section header image" /></div>

Redis, the in-memory data structure store, operates as a swift messenger,
delivering data at lightning speed. Access the realm of Redis 
via `C::Redis()->...`, a doorway to a universe where data traverses in real-time.

Access to redis is possible via `phpredis` and `predis`. PHP's native package will be prefered, if it is
available.

### Configuration:

Inscribe the connection runes in the `connections.yaml` scroll:

```yaml
# Redis
# ---------------------------------------------
redis:
  # Should redis be enabled?
  enabled: true
  # Driver to use: phpredis (only used if available), predis
  driver: phpredis
  scheme: tcp
  # Authentication
  host: '127.0.0.1'
  port: 6379
  password: ''
  # Prefix for all stored keys
  prefix: myapp_
  # Persistent connection
  persistent: true
```

### Engaging with Redis:

Engage with Redis directly, retrieving the ancient scripts:

```php
$value = C::Redis()->get('mykey');
```

or delve deeper into the native client to unveil more powers:

```php
C::Redis()->getClient()->hdel(...);
```

All common methods are available both ways.

Redis, the swift courier in the data realms, stands ready to heed your call, 
transcribing your commands into the ether of rapid data exchange.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Database module, your compass in the wilderness of data, is more than a mere library. 
It's a sage guiding you through the structured yet complex labyrinths of databases. 
With every method invocation, a path in the enigmatic forest of data clears, 
leading you to the sanctum of knowledge. As you venture deeper into the Charm framework, 
let the Database module be your lodestar, illuminating the way through the dark woods of queries, 
towards the enlightenment that the structured data beholds.

</div>
