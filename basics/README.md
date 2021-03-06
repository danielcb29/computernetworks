# Basics directory
This directory contains various programs which were extracted from these books

- Computer Networks a Top-down approach
- Python Network Programming Cookbook

As follows is presented the following topics

- A UDP Client/Server program
- A TCP Client/Server program

## A simple UDP client-server program

Client: ``UDPClient.py``

Server: ``UDPServer.py``

To run these programs open two terminals. In one terminal run ``python UDPServer.py``.
Go to the other terminal and run ``python UDPClient.py`` then follow the instructions.

## A simple TCP client-server program

Client: ``TCPClient.py``

Server: ``TCPServer.py``

To run these programs open two terminals. In one terminal run ``python TCPServer.py``.
Go to the other terminal and run ``python TCPClient.py`` then follow the instructions.

## Questions about UDP\* and TCP\* programs?

- What happen if the UDPClient.py is run before UDPServer.py?
- What happen if you run the UDPClient.py program, type a sentence and hit ``ENTER``
- What happen if the TCPClient.py is run before TCPServer.py?
- What happen if TCPServer.py is run then UDPClient.py? 
- What happen if UDPServer.py is run then TCPClient.py?
- What happen if you run two instances of TCPServer.py simultaneously? 
- What happen if you run two instances of UDPServer.py simultaneously? 
- Can you run TCPServer.py and UDPServer.py simultaneously?
- Do you remember this sentence ``serverSocket.bind(('',serverPort))``? What is the meaning of ``''``? 

## Another useful methods provided by socket

Open a terminal and type ``python``. 
A python shell should run ``>>>``. 
If you see the python shell then type the following commands

- ``socket.gethostname()``, returns the host name of the machine where this command is executed
- ``socket.gethostbyname('www.google.com')``, returns the IP of ``www.google.com``. What service was used to obtain that IP?

## Converting IP numbers to different formats
This program converts an IP address from string format to its hex representation and backwards.

```
import socket
from binascii import hexlify

def convert_ip4_address():
	for ip_addr in ['127.0.0.1', '192.168.0.1']:
		packed_ip_addr = socket.inet_aton(ip_addr)
		unpacked_ip_addr = socket.inet_ntoa(packed_ip_addr)
		print "IP Address: %s => Packed: %s, Unpacked: %s"%(ip_addr, hexlify(packed_ip_addr), unpacked_ip_addr)

convert_ip4_address()
```

## Printing the current time from the Internet time server

This program queries to a remote server for the local time (via NTP protocol) and prints the answer.

**NOTE** You probably must install the ``ntplib`` for Python before to run this code.
Open a terminal and run ``sudo pip install ntplib``.

```
import ntplib
from time import ctime

def print_time():
	ntp_client = ntplib.NTPClient()
	response = ntp_client.request('pool.ntp.org')
	print ctime(response.tx_time)

print_time()
```

## Finding a service name, given the port and protocol

This program shows how to know the name of a service given its port and protocol.

```
import socket

def find_service_name():
	protocolname = 'tcp'
	for port in [80, 25]:
		print "Port %s => service name %s"%(port, socket.getservbyport(port, protocolname))
	print "Port %s => service name %s"%(53, socket.getservbyport(53, 'udp'))

find_service_name()
```
