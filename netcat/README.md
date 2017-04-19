## netcat

[Netcat](http://man.openbsd.org/nc) is a networking utility for reading from and writing to network connections.

For Kaazing demos and tutorials this container is usually used to act as a TCP client in order to connect to a server.

```bash
$ docker run -it -rm kaazing/netcat 192.168.99.100 9000
```

where `192.168.99.100` is the IP address of your Docker host.
