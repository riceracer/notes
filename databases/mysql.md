## Log in to DB

    mysql <db_name> -u <user_name> -p
    
## Force TCP connection to localhost

This can help if you want to connect to a MySQL instance running in a docker container.
* Assumes you have port mapping in the container, e.g. 3306 -> 3306
* Must use ```-h 127.0.0.01``` instead of "localhost" because that forces it to use TCP instead of a socket

```
mysql DB_NAME -u USERNAME -p -h 127.0.0.1 -P 3306
```

## Show all tables

    show tables;

## describe table

    desc <table_name>;

## show create table SQL

    show create table <table_name>;

## Group by date of a datetime field

    select date(date_field), count(1) from my_table group by date(date_field);

## Show grants

    show grants;
    show grants for <USER>;

## MySQL export to CSV

First the user needs to have the FILE priveledge (or be root)

Log in as root

    GRANT FILE ON *.* TO '<USER>'@'%';
    exit

Log in as USER:

```
SELECT * from <TABLE>
INTO OUTFILE '/var/lib/mysql-files/output.csv'
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```

* The OUTFILE path needs to be in the "secure_file_priv" path. You can check what paths are there with this query:

```
SHOW VARIABLES LIKE "secure_file_priv";
+------------------+-----------------------+
| Variable_name    | Value                 |
+------------------+-----------------------+
| secure_file_priv | /var/lib/mysql-files/ |
+------------------+-----------------------+
```

## Select (approximate) row count of all tables in a DB

```
SELECT 
    table_name, 
    table_rows 
FROM 
    `information_schema`.`tables` 
WHERE 
    `table_schema` = 'DATABASE_NAME';
```

* replace DATABASE_NAME with the actual db name
* The row count isn't exactly right, but it will give a faster ballpark than querying each table.
* Some tables might report 0 records even if they have a few records.

## Dump table

See https://dev.mysql.com/doc/refman/5.7/en/mysqldump-sql-format.html (or equivalent for newer version) for details

```
mysqldump DB_NAME TABLE1 TABLE2 TABLE3

# Only dump all table definitions
mysqldump --default-character-set=utf8 --no-data -u DB_USER -p DB_NAME > /var/lib/mysql/backups/table_defs_only.sql

# Only dump data from specific tables
TABLE=foo
mysqldump --default-character-set=utf8 --no-create-info -u DB_USER -p DB_NAME $TABLE > /var/lib/mysql/backups/table_${TABLE}.sql

```
