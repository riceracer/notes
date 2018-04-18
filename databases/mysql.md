# MySQL

## Force TCP connection to localhost

This can help if you want to connect to a MySQL instance running in a docker container.
* Assumes you have port mapping in the container, e.g. 3306 -> 3306
* Must use ```-h 127.0.0.01``` instead of "localhost" because that forces it to use TCP instead of a socket

```
mysql iuu -u skylight -p -h 127.0.0.1 -P 3306
```
