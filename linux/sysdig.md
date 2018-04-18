# Sysdig

Capture and analyze kernel events - can be used to make pretty spectograms to plot performance issues.

    sudo apt-get install sysdig

Capture events:

    sudo sysdig -w trace.scap

Capture for specific container:

   sudo sysdig -w container.scap container.name=docker_container_name

Spectrogram!

    sudo sysdig -r trace.scap -c spectrogram evt.type=writev
    sudo sysdig -r trace.scap -c spectrogram evt.type=write
    sudo sysdig -r trace.scap -c spectrogram evt.type=lstat

Show top calls by time

```
sudo sysdig -r trace.scap -c topscalls_time

Time                Syscall             
--------------------------------------------------------------------------------
113.86s             futex
49.48s              epoll_wait
39.03s              poll
...
```

Top calls by count

```
sudo sysdig -r trace.scap -c topscalls
# Calls             Syscall             
--------------------------------------------------------------------------------
65924               ioctl
37238               recvmsg
28430               gettid
...
```

Many, many more examples here:
* https://github.com/draios/sysdig/wiki/sysdig-examples
