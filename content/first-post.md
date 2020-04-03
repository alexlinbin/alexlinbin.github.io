title: First Post on My Sweet New Blog
date: 2020-04-03 10:34:00
author: Your Name Here
# I am On My Way To Internet Fame and Fortune!
This is my first post on my new blog. While not super informative it
should convey my sense of excitement and eagerness to engage with you,
the reader!

```python
import struct
import socket

header_length = 4

listen_sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
listen_sock.bind(("127.0.0.1", 8889))
listen_sock.listen(10)


def pack_data(data):
    return struct.pack(">I", len(data)) + data


while True:
    sock, address = listen_sock.accept()
    header = sock.recv(header_length)
    body_length, = struct.unpack(">I", header)
    buffer = sock.recv(body_length)

    reply = b"you get me " + buffer
    print(pack_data(reply))
    sock.sendall(pack_data(reply))
    sock.close()

```
