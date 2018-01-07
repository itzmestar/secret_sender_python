# secret_sender_python

Program implements the following command-line interface: 
./packet_sender [ip_address] [interface] [type] [message]
program send the [message], encoded as described below, to the IP address specified by [ip_address] 
on physical interface [interface]. 
[type] specifies the type of packet that the IP datagram will hold, where [type] can be one of:
• 0: ICMP Echo Request Message
• 1: TCP SYN packet to port 80

Each byte of the message are sent in the IP layer of a packet 
(so one packet is sent for every byte of the message).
The message byte is encoded in the high 8 bits of the Identification field of the IP datagram. 
The lower 8 bits of the Identification field stay consistent, as they serve as the identifier of 
this message (and not all 1s, as noted below).
The byte number (the number of the byte from the message being sent) is encoded 
into the lower 8 bits of the Fragment Offset field (note this means that at most we can send 28 -1 size messages). 
Finally, when there are no more bytes to send, the highest bit of the Fragment Offset is set to 1 
and the lower 8 bits of the Fragment Offset field is set to the length of the message (total bytes sent).


Tested to work with:
Python 2.7.11 on ubuntu linux.



How to run the executable:
--------------------------
# ./packet_sender [ip_address] [interface] [type] [message]
Where :

        ip_address : Destination IP address
        
        interface  : Source ethernet interface
        
        type       : 0 -> ICMP Echo Request Message Or 1 -> TCP SYN packet to port 80
        
        message    : message to be sent in packet

All of the options are mandotary.
---------------------------
Example of a run:
# ./packet_sender.py 192.168.43.167 eth0 0 test

Sending IPv4/ICMP packet:

###[ IP ]###
  version   = 4
  ihl       = None
  tos       = 0x0
  len       = None
  id        = 29735
  flags     = DF
  frag      = 0
  ttl       = 64
  proto     = icmp
  chksum    = None
  src       = 192.168.43.92
  dst       = 192.168.43.167
  \options   \
###[ ICMP ]###
     type      = echo-request
     code      = 0
     chksum    = None
     id        = 0x27
     seq       = 0x1
.
Sent 1 packets.

Sending IPv4/ICMP packet:

###[ IP ]###
  version   = 4
  ihl       = None
  tos       = 0x0
  len       = None
  id        = 25895
  flags     = DF
  frag      = 1
  ttl       = 64
  proto     = icmp
  chksum    = None
  src       = 192.168.43.92
  dst       = 192.168.43.167
  \options   \
###[ ICMP ]###
     type      = echo-request
     code      = 0
     chksum    = None
     id        = 0x27
     seq       = 0x2
.
Sent 1 packets.

Sending IPv4/ICMP packet:

###[ IP ]###
  version   = 4
  ihl       = None
  tos       = 0x0
  len       = None
  id        = 29479
  flags     = DF
  frag      = 2
  ttl       = 64
  proto     = icmp
  chksum    = None
  src       = 192.168.43.92
  dst       = 192.168.43.167
  \options   \
###[ ICMP ]###
     type      = echo-request
     code      = 0
     chksum    = None
     id        = 0x27
     seq       = 0x3
.
Sent 1 packets.

Sending IPv4/ICMP packet:

###[ IP ]###
  version   = 4
  ihl       = None
  tos       = 0x0
  len       = None
  id        = 29735
  flags     = DF
  frag      = 3
  ttl       = 64
  proto     = icmp
  chksum    = None
  src       = 192.168.43.92
  dst       = 192.168.43.167
  \options   \
###[ ICMP ]###
     type      = echo-request
     code      = 0
     chksum    = None
     id        = 0x27
     seq       = 0x4
.
Sent 1 packets.

Sending IPv4/ICMP packet:

###[ IP ]###
  version   = 4
  ihl       = None
  tos       = 0x0
  len       = None
  id        = 39
  flags     = DF
  frag      = 4100
  ttl       = 64
  proto     = icmp
  chksum    = None
  src       = 192.168.43.92
  dst       = 192.168.43.167
  \options   \
###[ ICMP ]###
     type      = echo-request
     code      = 0
     chksum    = None
     id        = 0x27
     seq       = 0x5
.
Sent 1 packets.


