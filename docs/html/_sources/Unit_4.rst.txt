.. _unit4:

Unit 4 - Networking 1
~~~~~~~~~~~~~~~~~~~~~

Computing devices directly deliver messages for other devices on the same network through switches. Switches connect devices of the same network together. However, computing devices rely on a router to communicate with devices on different networks.

.. _unit4_mac_and_ip:

MAC and IP Addresses
--------------------

.. _unit4_mac:

**MAC -- media access control.**

MAC addresses are physical addresses are physical addresses burned into the NIC (network interface card) which is the chip through which all network communications enters and exits a machine. MAC addresses are 48 bits long, represented with 12 base 16 hexadecimal characters, and are separated into two sections. The first six hex characters represent the manufacturer of the NIC assigned by the I triple E -- the Institute of Electrical and Electronic Engineers. The last six hex characters, the device ID, is a unique value assigned to a manufacturer to each of its NICs. MAC addresses are unique.

.. _unit4_ip:

**IP -- internet protocol.**

IPv4 addresses are logical addresses, bound to NICs through software. They are 32 bit addresses, represented with four base 10 decimal numbers, and are also separated into two sections. The first section represents the network ID, the starting string of bits that all nodes on a shared network have in common. The second section represents a host ID, for each host on a shared network. An entity known as a subnet mask (another 32 bit value) identifies where the breakup of network ID and host ID occurs.


.. _unit_4_subnet_mask:

Subnet Masks
============

Host A with IP address 10.10.1.1 wants to communicate with host B whose IP address is 10.10.1.2. The host A will take its IP address in subnet mask and perform a boolean **AND** operation. All 32 bits of the IP address are lined up with the 32 bits of the subnet mask. In this case, the subnet mask of the source 10.10.1.1 is 255.255.255.0 in base 10. In binary, it looks like 24 ones followed by 8 zeros. This means that the first 24 of the 32 bits are network bits and are shared by every device on this network. The last eight bits are host bits and are unique in entirety to each host on this network. 

::
        Host A
        10.10.1.1       00001010.00001010.00000001.0000001      <- Host A IP address
        255.255.255.0   11111111.11111111.11111111.0000000      <- Subnet Mask
                        ----------------------------------
        10.10.1.0       00001010.00001010.00000001.0000000      <- Network Identifier

                        ^^^^^^^^
                         Octet

Each of the four base 10 numbers is known as an octet because each number is represented by eight bits in binary. Subnet masks can span multiple octets and need not be contained to a multiple of eight bits.

No matter how many host bits are in an IP address, if they are all zeros that represents a **network identifier and cannot be assigned to a host**. They can't be all ones either because when all host bits are set to one that represents a **network broadcast address cannot be assigned to hosts**.

::
        10.10.1.255     00001010.00001010.00000001.11111111      <- Network Broadcast

If the host A (source) needs to determine if the host B (destination) is on the same network or a different one by performing a second boolean **AND** operation. The source takes the destination IP address and logically ends it with the sources own subnet mask.

::
        Host B
        10.10.1.2       00001010.00001010.00000001.0000010      <- Host B IP address
        255.255.255.0   11111111.11111111.11111111.0000000      <- Subnet Mask
                        ----------------------------------
        10.10.1.0       00001010.00001010.00000001.0000000      <- Network Identifier

This lets the source know that the destination is on the same network and traffic can be delivered directly. The destination's IP address is either known by the source or resolved from its name using DNS, domain name system.
