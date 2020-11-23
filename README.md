# ws2udp

A WebSocket to UDP proxy. 

## Installation


## Usage:

```
$ ws2udp
WebSocket to UDP proxy

optional arguments:
  -h, --help           show this help message and exit
  --udp-addr UDP_ADDR  Address of the UDP receiver for broadcasting messages (default=localhost)
  --udp-port UDP_PORT  Port of the UDP receiver (default=57142)
  --addr ADDR          WebSocket address to listen (default=0.0.0.0)
  --port PORT          WebSocket port to listen (default=8765)
```

The server expects binary messages following the format:

`*address_length*(uint32)*address*(string)*port*(uint32)*data*`

* _address_length_ is an integer representing the total length of the address
* _address_ the address where to forward the data as a string (example: localhost)
* _port_ as an integer
* _data_ the original message data

For example, to send the message `hello world` to `localhost:57120`, one would send:

`b'\x09\x00\x00\x00localhost\x20\xdf\x00\x00hello, world'`

The first 4 bytes `b'\t\x00\x00\x00` represents 9, then comes `b'localhost'` and lastly `b'\x20\xdf\x00\x00'` for 57120. Whatever comes after this is forwarded.
