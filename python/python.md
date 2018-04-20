# argparse - standard argument parsing

* https://docs.python.org/3/howto/argparse.html

```
import argparse


if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument("source")
    parser.add_argument("destination")
    args = parser.parse_args()
    print("{} to {}".format(args.source, args.destination))
```

# expiringdict

Simple in memory cache with expiring entries.

* https://pypi.python.org/pypi/expiringdict/1.1.2

```
from expiringdict import ExpiringDict
cache = ExpiringDict(max_len=100, max_age_seconds=10)
cache["key"] = "value"
cache.get("key")
```

# iterate over multiple lists together

Use builtin function `zip()`

```
list1 = range(1,6)
list2 = range(6,11)
list3 = range(11,16)
for i, j, k in zip(list1, list2, list3):
    print(i, j, k)
```

# mysql db connection

* pymysql - https://pymysql.readthedocs.io/en/latest/

Create Connection:
```
import pymysql

connection = pymysql.connect(
    host='HOSTNAME',
    user='USERNAME',
    password='PASSWORD',
    db='DBNAME',
    charset='utf8mb4',
    cursorclass=pymysql.cursors.DictCursor)
```

Query:
```
with connection.cursor() as cursor:
    sql = "SELECT * from MYTABLE LIMIT 10;"
    cursor.execute(sql)
    results = cursor.fetchall()
    for row in results:
        print(row['fieldname1'], row)
```

# MySQL to Pandas DataFrame

Open a connection, like using pymsql, then:

```
import pandas as pd
sql = "SELECT * from TABLENAME where foo = %s"
df = pd.read_sql(sql, connection, params=['bar'])
```
