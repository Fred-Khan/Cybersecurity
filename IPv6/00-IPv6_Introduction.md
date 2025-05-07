IPv6 Addresses
==============
1. IPv6 addresses are written using hexadecimal, as opposed to dotted decimal in IPv4.
2. Because a hexadecimal digit uses 4 bits this means that an IPv6 address consists of 32 hexadecimal numbers as opposed to 32 binary numbers in IPv4.
3. An Ipv6 address uses 128 bits.
4. These digits are grouped in 4’s giving 8 groups or blocks. The groups are written with a : (colon) as a separator.
5. Here is an IPv6 address example: 
	
	2001:0:9D38:6AB8:1C48:3A1C:A95A:B1C2

6. The first 64 bits are used for routing of which:
 a. The first 48 bits is the routing prefix known as the Global Unicast Address.
 b. The next 16 bits is used for the Subnet ID.


7. The are 3 type of IPv6 addresses:
a. Global Unicast Address –Scope Internet- routed on Internet
b. Link Local – Scope network link- Not Routed internally or externally.
c. Unique Local — Scope Internal Network or VPN internally routable, but Not routed on Internet
d. Loop Back

A. Global and Public Addresses
===============================
Global addresses are routable on the internet and start with 2001.

These addresses are known as global Unicast addresses and are the equivalent of the public addresses of IPv4 networks.

The Internet authorities allocate address blocks to ISPs who in turn allocate them to their customers.

See: https://www.iana.org/assignments/ipv6-unicast-address-assignments/ipv6-unicast-address-assignments.xhtml


B. Internal Addresses- Link Local and Unique Local
==================================================
In IPv4 internal addresses use the reserved number ranges 10.0.0.0/8, 172.16.0.0/12 and 192.168.0.0/16 and 169.254.0.0/16.

These addresses are not routed on the Internet and are reserved for internal networks.

IPv6 also has two Internal address types.

1. Link Local
2. Unique Local


B-1. Link Local
===============
These are meant to be used inside an internal network, and again they are not routed on the Internet.

It is equivalent to the IPv4 address 169.254.0.0/16 which is allocated on an IPv4 network when no DHCP server is found.

Link local addresses start with fe80

They are restricted to a link and are not routed on the Internal network or the Internet.

Link Local addresses are self assigned i.e. they do not require a DHCP server.

A link local address is required on every IP6 interface even if no routing is present.


B-2. Unique Local
=================
Unique Local are meant to be used inside an internal network.

They are routed on the Internal network but not routed on the Internet.

They are equivalent to the IPv4 addresses are 10.0.0.0/8, 172.16.0.0/12 and 192.168.0.0/16

The address space is divided into two /8 spaces: fc00::/8 for globally assigned addressing, and fd00::/8 for locally assigned addressing.

Distinction between FC00::/8 and FD00::/8
-----------------------------------------
FC00::/8: This part of the Unique Local Addresses (ULA) space was initially intended to be managed centrally with allocations being done by a registry. However, this central allocation has not been implemented, and as a result, addresses from the FC00::/8 range are not currently being used.

FD00::/8: Addresses within the FD00::/8 range are intended to be generated locally without a central registry. This makes them more commonly used in practice. The addresses are pseudo-randomly generated to ensure they are unique within the organization.

Therefore, manual assignment by an organisation of private IPv6 address should use the fd00 prefix.

Example:
	FD00:1234:5678:9ABC:DEF0:1234:5678:9ABC




IPV6 Addressing Scheme
======================

	2001:8003:500a:8001:e772:2e08:1def:7f8f

	2001:0DB8:4545:003:0200:F8FF:FE21:67CF
	\____________/ \_/ \_________________/
	      A		B	    C

A: Routing Prefix
B: Subnet ID
C: Interface ID


Routing Prefix sub-schema
=========================

2001:0DB8 - comes from Internet Registry (5 worldwide)
xxxx:xxxx:4545 - Region / Site added by ISP.

Global Routing Prefix would be: 2001:0DB8:4545 / 48

Subnets from the Global Routing Prefix of 2001:0DB8:4545 / 48
==============================================================

2001:0DB8:4545:0000 : 0000:0000:0000:0000 / 64 1st Subnet
...
2001:0DB8:4545:FFFF : 0000:0000:0000:0000 / 64 65,536th Subnet ie 2^16 = 65536


Small end user might receive a /60 IPv6 from their ISP
======================================================

  60 bits = /60
<---------------->
2001:ACAD:1234:1230 : 0000:0000:0000:0000

The subnet ID would be the 0 in :1230 ie 4 bits available to subnet.
Therefore, you could have 2^4 = 16 /64 subnets in a /60 network
The subnets would:
- Start at 2001:ACAD:1234:1230 : 0000:0000:0000:0000 (1st subnet)
- End at   2001:ACAD:1234:123F : 0000:0000:0000:0000 (16th subnet)



What about when a prefix is not a multiple of 4 or 16?
======================================================

Example:

2001:0DB8:4545:5003:0200:F8FF:FE21:67CF /53

 16 : 16 : 16 : 5 

Prefix would be: 2001:0DB8:4545:5000 : 0:0:0:0 / 53


 


Example Subnetting using Unique Local Addressing scheme
=======================================================
Contoso Corp - IPv6 Unique Local Address Assignment Site

IPv6 Unique Local Address Range Assignment

Sydney
FD6D:8D64:AF0C::/64

Melbourne
FD6D:8D64:AF0C:1::/64

Brisbane
FD6D:8D64:AF0C:2::/64

Adelaide
FD6D:8D64:AF0C:3::/64

			
