# TCP_generator

Follow these instructions to build the tcp generator using DPDK 22.11 and CloudLab nodes

## Building

> ** Make sure that `PKG_CONFIG_PATH` is configured properly. **

```bash
git clone https://github.com/carvalhof/tcp_generator
cd tcp_generator
make
```

## Running

> ** Make sure that `LD_LIBRARY_PATH` is configured properly. **

```bash
sudo ./build/tcp-generator -a 41:00.0 -n 4 -c 0xff -- -r $RATE -f $FLOWS -s $SIZE -t $DURATION -q $QUEUES -c $ADDR_FILE -o $OUTPUT_FILE
```

> ** Example **

```bash
sudo ./build/tcp-generator -a 41:00.0 -n 4 -c 0xff -- -r 100000 -f 1 -s 128 -t 10 -q 1 -c addr.cfg -o output.dat
```

### Parameters

- `$RATE` : packet rate in _pps_
- `$FLOWS` : number of flows
- `$SIZE` : packet size in _bytes_
- `$DURATION` : duration of execution in _seconds_ (we double for warming up)
- `$QUEUES` : number of RX/TX queues
- `$ADDR_FILE` : name of address file (_e.g.,_ 'addr.cfg')
- `$OUTPUT_FILE` : name of output file containg the latency for each packet


### _address file structure_

```
[ethernet]
src = 0c:42:a1:8c:db:f4
dst = 0c:42:a1:8c:dc:1c

[ipv4]
src = 192.168.1.2
dst = 192.168.1.1

[tcp]
dst = 12345

[server]
nr_servers = 1
```