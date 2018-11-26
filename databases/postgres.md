## Connect to remote DB

    psql DB_NAME DB_USER -h HOSTNAME

## Turn off pager

    \pset pager off

## Toggle query timing

    \timing

## Get date from timestamp

    table.column_name::date = '2018-01-01'

## Get hour from timestamp

    date_part('hour', table.column_name)

## Get information about all foreign keys linking into a target table

```
SELECT
  tc.constraint_name, tc.table_name, kcu.column_name,
  ccu.table_name AS foreign_table_name,
  ccu.column_name AS foreign_column_name                                                                                                                                                   FROM
  information_schema.table_constraints AS tc
JOIN information_schema.key_column_usage AS kcu
ON tc.constraint_name = kcu.constraint_name
JOIN information_schema.constraint_column_usage AS ccu
ON ccu.constraint_name = tc.constraint_name
WHERE constraint_type = 'FOREIGN KEY' AND ccu.table_name='target_table';
```

## Regexp_matches to get matching pattern from a field

```
select (regexp_matches('foo:baz:bar:car', 'foo:([^:]+):.*'))[1] as thing2;
```

* returns "baz"

## Select output as CSV format (unsafe - not escaped correctly)

```
\f ','
\a
SELECT 1 as foo, 2 as bar, 3 as baz;
```

## Write query to CSV output, properly escaped, with header

```
COPY (

SELECT * FROM bar

) To '/tmp/output.csv' With CSV HEADER;
```

## Geometry: collect many geometric fields into a group by query

```
SELECT 
  name
  ,ST_AsText(ST_Collect(geometry_field)) as collected
FROM foo
GROUP BY 1;
```

## Query for locked connections

```
select pid, client_addr, backend_start, state, wait_event_type, substring(query, 0, 100) from pg_stat_activity where state = 'active';
```

## Abort locked connection by pid

First try:

    select pg_cancel_backend(<PID>)

Fallback:

    select pg_terminate_backend(<PID>)
 
## Fast query partition table counts

```
select * from schema_v('TABLENAME_partition');
```
