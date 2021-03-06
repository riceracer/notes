# Python

Currently these notes apply mostly to Python 3.5 or 3.6.

## Generic script main method

```
def run():
    print("hello")


if __name__ == '__main__':
    run()
```

## argparse - standard argument parsing

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

## read csv

```
import csv


def run(input_csv):
    with open(input_csv, 'r', newline='') as file:
        reader = csv.DictReader(file)
        for row in reader:
            print(row['key1'], row['key2'])
```

## expiringdict

Simple in memory cache with expiring entries.

* https://pypi.python.org/pypi/expiringdict/1.1.2

```
from expiringdict import ExpiringDict
cache = ExpiringDict(max_len=100, max_age_seconds=10)
cache["key"] = "value"
cache.get("key")
```

## json

Add a to_json method to objects for basic json serialization. (not foolproof, but quick and easy hack):

```
import datetime
import uuid
from dateutil.tz import tzutc
import json

        
class ToJsonMixin:
    def to_json(self):
        def json_serialize(obj):
            if isinstance(obj, datetime.datetime):
                return obj.astimezone(tzutc()).strftime("%Y-%m-%dT%H:%M:%SZ")
            elif isinstance(obj, uuid.UUID):
                return str(obj)
            elif isinstance(obj, decimal.Decimal):
                return str(obj)
            elif hasattr(obj, '__dict__'):
                return obj.__dict__
            else:
                return str(obj)
        return json.dumps(self, default=json_serialize, separators=(',', ':'))
        

class MyClass(ToJsonMixin):
    def __init__(self, foo, bar):
        self.foo = foo
        self.bar = bar
```


## iterate over multiple lists together

Use builtin function `zip()`

```
list1 = range(1,6)
list2 = range(6,11)
list3 = range(11,16)
for i, j, k in zip(list1, list2, list3):
    print(i, j, k)
```

## mysql db connection

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

## MySQL to Pandas DataFrame

Open a connection, like using pymysql, then:

```
import pandas as pd
sql = "SELECT * from TABLENAME where foo = %s"
df = pd.read_sql(sql, connection, params=['bar'])
```

## Matplotlib virtual env hack on mac

* https://matplotlib.org/faq/osx_framework.html

```
python -m venv my-virtualenv
source my-virtualenv/bin/activate
```

## PIL - Python Imaging Library

### Get image dimensions

```
from PIL import Image
img = Image.open(image_filename)
width, height = img.size
```

## Function timer

```
from functools import wraps
import time


def func_timer(printer=print, log_on_start=True):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            if log_on_start:
                printer("func_timer: Started {}".format(func.__name__))
            start = time.time()
            start_pt = time.process_time()
            result = func(*args, **kwargs)
            end = time.time()
            end_pt = time.process_time()
            delta = end - start
            delta_pt = end_pt - start_pt
            printer("func_timer: Finished {} time={:.3f} ptime={:.3f}".format(func.__name__, delta, delta_pt))
            return result
        return wrapper
    return decorator
    
   
@func_timer()
def foo():
    pass
    
@func_timer(log.info, False)
def bar():
    pass
```

## built-in functions

### dir

* list contents (methods/attributes of some object)

```
foo = SomeObject()
dir(foo)
```

## Run ipython in virtual enviornment

Add this to .bashrc or whatever:

```
alias ipy="python -c 'import IPython; IPython.terminal.ipapp.launch_new_instance()'"
```

## None-safe min/max

```
foo = [-10, 30, None, -50, 100, 15, None]
min(x for x in foo if x is not None)
max(x for x in foo if x is not None)
```

## Read from file or stdin

```
import fileinput

for line in fileinput.input():
    line = line.rstrip()
    print "l={}".format(line)
   
```
