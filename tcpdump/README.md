# tcpdump

[tcpdump](http://www.tcpdump.org/) is a networking utility that prints out a description of the contents of packets on a network interface.

For Kaazing demos and tutorials, this container will let you capture network traffic that occurs inside the docker containers for analysis with Wireshark. You can save a dumpfile to open in Wireshark after the fact, or you can monitor the traffic in real time with Wireshark.

## Usage with Docker

1. Start your Docker containers or Docker Compose suite in the normal way.

2. Then start the container to capture network traffic:

    ```bash
    $ docker run --rm --net=host -v $PWD/tcpdump:/tcpdump kaazing/tcpdump
    ```

    This will save network traffic in `tcpdump/tcpdump.pcap` of the current directory.

    If you want to save to a different location, change `$PWD/tcpdump` volume to a directory where you'd like the dumpfile to be saved. On Linux and Mac you can use the `$PWD` to refer to the current directory. Docker expects an absolute path here, which is why you can't use `./`.

3. You can watch the traffic live in Wireshark using the following command as you run your scenario. This will open Wireshark where you can see the packets, apply filters, etc:

    ```bash
    tail -c +1 -f tcpdump/tcpdump.pcap | wireshark -k -i -
    ```

    Alternatively, you can simply open `tcpdump/tcpdump.pcap` as a file using Wireshark after you have finished capturing.

## Usage with Docker Compose

1. Add the following service to your `docker-compose.yml` file.

    ```
      tcpdump:
        image: kaazing/tcpdump
        network_mode: "host"
        volumes:
          - ./tcpdump:/tcpdump
    ```

2. Start your Docker Compose suite.

   The `tcpdump` service will save network traffic in `tcpdump/tcpdump.pcap` of the current directory.

3. You can watch the traffic live in Wireshark using the following command as you run your scenario. This will open Wireshark where you can see the packets, apply filters, etc:

    ```bash
    tail -c +1 -f tcpdump/tcpdump.pcap | wireshark -k -i -
    ```

    Alternatively, you can simply open `tcpdump/tcpdump.pcap` as a file using Wireshark after you have finished capturing.

## Changing the parameters

You can specify your own parameters, overriding the default.

### Docker

Specify your parameters:

```bash
docker run --rm --net=host -v $PWD/tcpdump:/tcpdump kaazing/tcpdump -v -i any -w myapp.pcap
```

### Docker Compose

Add the `command` tag with your parameters to the service:

```
  tcpdump:
    image: kaazing/tcpdump
    network_mode: "host"
    volumes:
      - ./tcpdump:/tcpdump
    command: [ "-C", "100", "-W", "2", "-v", "-i", "any", "-w", "/tcpdump/myapp.pcap" ]
```
