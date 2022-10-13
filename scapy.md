## Exercise
# Part 0

In a second tab I ping google.com, and in the main tab I open scapy (with sudo) and run `capture = sniff(count=10)`
Afterwards I can run `capture.show()` to see all of the packets I intercepted.

```bash
>>> capture = sniff(count=10)
>>> capture.show()
0000 Ether / IP / ICMP 192.168.154.99 > 192.12.94.30 echo-request 0 / Raw
0001 Ether / IP / ICMP 192.12.94.30 > 192.168.154.99 echo-reply 0 / Raw
0002 Ether / IP / ICMP 192.168.154.99 > 192.12.94.30 echo-request 0 / Raw
0003 Ether / IP / ICMP 192.12.94.30 > 192.168.154.99 echo-reply 0 / Raw
0004 Ether / IP / ICMP 192.168.154.99 > 192.12.94.30 echo-request 0 / Raw
0005 Ether / IP / ICMP 192.12.94.30 > 192.168.154.99 echo-reply 0 / Raw
0006 Ether / IP / ICMP 192.168.154.99 > 192.12.94.30 echo-request 0 / Raw
0007 Ether / IP / ICMP 192.12.94.30 > 192.168.154.99 echo-reply 0 / Raw
0008 Ether / IP / ICMP 192.168.154.99 > 192.12.94.30 echo-request 0 / Raw
0009 Ether / ARP who has 192.168.144.1 says 192.168.154.99
```

## Lab
# Part 1

```bash
>>> ofp = IP()
>>> ofp.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= hopopt
  chksum= None
  src= 127.0.0.1
  dst= 127.0.0.1
  \options\
```

# Part 2

```bash
>>> ofp = IP(dst="130.108.128.200")
>>> ofp.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= hopopt
  chksum= None
  src= 192.168.154.99
  dst= 130.108.128.200
  \options\
```

# Part 3

```bash
>>> ofudp = ofp/UDP()
>>> ofp.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= hopopt
  chksum= None
  src= 192.168.154.99
  dst= 130.108.128.200
  \options\

>>> ofudp.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= udp
  chksum= None
  src= 192.168.154.99
  dst= 130.108.128.200
  \options\
###[ UDP ]###
     sport= domain
     dport= domain
     len= None
     chksum= None
```

# Part 4

```bash
>>> ofdnsp=ofudp/DNS()
>>> ofdnsp.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= udp
  chksum= None
  src= 192.168.154.99
  dst= 130.108.128.200
  \options\
###[ UDP ]###
     sport= domain
     dport= domain
     len= None
     chksum= None
###[ DNS ]###
        id= 0
        qr= 0
        opcode= QUERY
        aa= 0
        tc= 0
        rd= 1
        ra= 0
        z= 0
        ad= 0
        cd= 0
        rcode= ok
        qdcount= 0
        ancount= 0
        nscount= 0
        arcount= 0
        qd= None
        an= None
        ns= None
        ar= None
```

# Part 5

```bash
>>> ofdns= ofudp/DNS(rd=1,qd=DNSQR(qname="www.google.com"))
>>> ofdns.show()
###[ IP ]###
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags=
  frag= 0
  ttl= 64
  proto= udp
  chksum= None
  src= 192.168.154.99
  dst= 130.108.128.200
  \options\
###[ UDP ]###
     sport= domain
     dport= domain
     len= None
     chksum= None
###[ DNS ]###
        id= 0
        qr= 0
        opcode= QUERY
        aa= 0
        tc= 0
        rd= 1
        ra= 0
        z= 0
        ad= 0
        cd= 0
        rcode= ok
        qdcount= 1
        ancount= 0
        nscount= 0
        arcount= 0
        \qd\
         |###[ DNS Question Record ]###
         |  qname= 'www.google.com'
         |  qtype= A
         |  qclass= IN
        an= None
        ns= None
        ar= None
```

# Part *Special*

```bash
ofdns= (IP(dst="130.108.128.200")/UDP())/DNS(rd=1,qd=DNSQR(qname="www.google.com"))
```

# Part 6

```bash
>>> response = sr(ofdns)
Begin emission:
.Finished sending 1 packets.
*
Received 2 packets, got 1 answers, remaining 0 packets
>>> response[0].show()
0000 IP / UDP / DNS Qry "b'www.google.com'"  ==> IP / UDP / DNS Ans "142.250.191.132"
```