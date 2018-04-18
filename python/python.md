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
