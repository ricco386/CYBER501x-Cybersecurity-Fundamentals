Unit 4 - Networking 1
~~~~~~~~~~~~~~~~~~~~~

Computing devices directly deliver messages for other devices on the same network through switches. Switches connect devices of the same network together. However, computing devices rely on a router to communicate with devices on different networks.

MAC and IP Addresses
--------------------

**MAC -- media access control.**

MAC addresses are physical addresses are physical addresses burned into the NIC (network interface card) which is the chip through which all network communications enters and exits a machine. MAC addresses are 48 bits long, represented with 12 base 16 hexadecimal characters, and are separated into two sections. The first six hex characters represent the manufacturer of the NIC assigned by the I triple E -- the Institute of Electrical and Electronic Engineers. The last six hex characters, the device ID, is a unique value assigned to a manufacturer to each of its NICs. MAC addresses are unique.

**IP -- internet protocol.**

IPv4 addresses are logical addresses, bound to NICs through software. They are 32 bit addresses, represented with four base 10 decimal numbers, and are also separated into two sections. The first section represents the network ID, the starting string of bits that all nodes on a shared network have in common. The second section represents a host ID, for each host on a shared network. An entity known as a subnet mask (another 32 bit value) identifies where the breakup of network ID and host ID occurs.

Subnet Masks
============
