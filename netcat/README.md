# netcat

[Netcat](http://man.openbsd.org/nc) is a networking utility for reading from and writing to network connections.

For Kaazing demos and tutorials, this container is usually used to act as a TCP client in order to connect to a server.

## Usage

```bash
$ docker run -it --rm kaazing/netcat 192.168.99.100 9000
```

In the command above:

* Change `192.168.99.100` the IP address of your Docker host.

* Change `9000` to the port exposed by the container you want to connect to.

## Usage with a Docker or Docker Compose network

```bash
$ docker run -it --rm --net=myproject_mynet kaazing/netcat example.com 9000
```

In the command above:

* `myproject_mynet` to the name of your network. You can see the list of networks with `$ docker network ls`.

* Change `example.com` to a hostname that's recognized on your Docker or Docker Compose network.

* Change `9000` to the port you want to connect to.
