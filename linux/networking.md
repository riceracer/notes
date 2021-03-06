# Networking

## Show host IP Address

    hostname -i
    hostname -I

* The capital-I form shows all ip addresses - useful if the first command just returns the loopback address.

## Show ports in use

    sudo lsof -i

## netstat

    sudo netstat -p

* -p - show process id/name for each connection

## Dig to find ip address for hostname

    dig +short www.google.com

## Dig to find the hostname for an ip address (reverse lookup)

    dig -x IPADDRESS

## SSH Tunnel

Create a tunnel between local and remove host and port

```
LOCALPORT=1234
REMOTEHOST=foo-bar
REMOTEPORT=1234
REMOTEUSER=foo

ssh -L $LOCALPORT:$REMOTEHOST:$REMOTEPORT $REMOTEUSER@$REMOTEHOST
```
