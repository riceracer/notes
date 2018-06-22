# Networking

## Show ports in use

    sudo lsof -i

## netstat

    sudo netstat -p

* -p - show process id/name for each connection

## Dig to find ip address for hostname

    dig +short www.google.com

## SSH Tunnel

Create a tunnel between local and remove host and port

```
LOCALPORT=1234
REMOTEHOST=foo-bar
REMOTEPORT=1234
REMOTEUSER=foo

ssh -L $LOCALPORT:$REMOTEHOST:$REMOTEPORT $REMOTEUSER@$REMOTEHOST
```
