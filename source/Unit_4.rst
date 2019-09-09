.. _unit4:

Unit 4 - Networking 1
~~~~~~~~~~~~~~~~~~~~~

Computing devices directly deliver messages for other devices on the same network through switches. Switches connect devices of the same network together. However, computing devices rely on a router to communicate with devices on different networks.

.. _unit4_mac:

MAC Address
-----------

MAC (media access control) addresses are physical addresses are physical addresses burned into the NIC (network interface card) which is the chip through which all network communications enters and exits a machine. MAC addresses are 48 bits long, represented with 12 base 16 hexadecimal characters, and are separated into two sections. The first six hex characters represent the manufacturer of the NIC assigned by the I triple E -- the Institute of Electrical and Electronic Engineers. The last six hex characters, the device ID, is a unique value assigned to a manufacturer to each of its NICs. MAC addresses are unique.

.. _unit4_ip:

IP Address
----------

IPv4 (internet protocol) addresses are logical addresses, bound to NICs through software. They are 32 bit addresses, represented with four base 10 decimal numbers, and are also separated into two sections. The first section represents the network ID, the starting string of bits that all nodes on a shared network have in common. The second section represents a host ID, for each host on a shared network. An entity known as a :ref:`unit4_subnet_mask` (another 32 bit value) identifies where the breakup of network ID and host ID occurs.

.. _unit4_subnet_mask:

Subnet Mask
-----------

Host A with :ref:`unit4_ip` 10.10.1.1 wants to communicate with host B whose :ref:`unit4_ip` is 10.10.1.2. The host A will take its :ref:`unit4_ip` in subnet mask and perform a boolean **AND** operation. All 32 bits of the :ref:`unit4_ip` are lined up with the 32 bits of the subnet mask. In this case, the subnet mask of the source 10.10.1.1 is 255.255.255.0 in base 10. In binary, it looks like 24 ones followed by 8 zeros. This means that the first 24 of the 32 bits are network bits and are shared by every device on this network. The last eight bits are host bits and are unique in entirety to each host on this network. 

.. sourcecode::

        Host A
        10.10.1.1       00001010.00001010.00000001.0000001      <- Host A IP address
        255.255.255.0   11111111.11111111.11111111.0000000      <- Subnet Mask
                        ----------------------------------
        10.10.1.0       00001010.00001010.00000001.0000000      <- Network Identifier

                        ^^^^^^^^
                         Octet

Each of the four base 10 numbers is known as an octet because each number is represented by eight bits in binary. Subnet masks can span multiple octets and need not be contained to a multiple of eight bits.

No matter how many host bits are in an :ref:`unit4_ip`, if they are all zeros that represents a **network identifier and cannot be assigned to a host**. They can't be all ones either because when all host bits are set to one that represents a **network broadcast address cannot be assigned to hosts**.

.. sourcecode::

        10.10.1.255     00001010.00001010.00000001.11111111      <- Network Broadcast

If the host A (source) needs to determine if the host B (destination) is on the same network or a different one by performing a second boolean **AND** operation. The source takes the destination :ref:`unit4_ip` and logically ends it with the sources own subnet mask.

.. sourcecode::

        Host B
        10.10.1.2       00001010.00001010.00000001.0000010      <- Host B IP address
        255.255.255.0   11111111.11111111.11111111.0000000      <- Subnet Mask
                        ----------------------------------
        10.10.1.0       00001010.00001010.00000001.0000000      <- Network Identifier

This lets the source know that the destination is on the same network and traffic can be delivered directly. The destination's :ref:`unit4_ip` is either known by the source or resolved from its name using DNS, domain name system.

.. note::

        Linux has a useful tool for calculating subnet masks: ``ipcalc``

.. _unit4_local_communication:

Local Communication
-------------------

.. _unit4_arp:

Address Resolution Protocol
===========================

For local traffic, the source needs the :ref:`unit4_mac` of the destination. The source puts the actual traffic on hold and sends out a broadcast message using a protocol known as ARP, address resolution protocol. ARP is meant to resolve a known :ref:`unit4_ip` to the :ref:`unit4_mac` that it is bound to in software.

The message in the ARP request explains that host A 10.10.1.1 is looking for them :ref:`unit4_mac` of 10.10.1.2. All devices on the network not only see this ARP request but they read it as well. Every device, except Host B discards the message. Host B 10.10.1.2 sends an ARP reply back to host A 10.10.1.1. The **ARP reply is unicast**, which means it only goes to 10.10.1.1 and is not broadcasted to the network. In the ARP request, the source listed its :ref:`unit4_mac` so the destination didn't need to broadcast to find out the sources :ref:`unit4_mac`.

.. note::

        Broadcast on networks are bad. Unfortunately, in the world of IPv4, there is no other way to do this.

After the ARP reply comes back to host A with host B's :ref:`unit4_mac`, host A can now fill-in the destination's :ref:`unit4_mac` and send the traffic. The source and destination :ref:`MAC addresses <unit4_mac>` are two of the fields found in the `Layer 2 <https://en.wikipedia.org/wiki/Data_link_layer>`_ `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ while the source and destination :ref:`IP addresses <unit4_ip>` are a couple of the fields in the IP packet.

.. _unit4_remote_communication:

Remote Communication
--------------------

Host A, the source, once again performs the boolean **AND** operation to determine that its network ID is 10.10.1.0. The destination :ref:`unit4_ip` is 10.10.4.1, host X. Using the :ref:`source mask <unit4_subnet_mask>` of 255.255.255.0, the second boolean **AND** operation results in a destination network ID of 10.10.4.0. The two network IDs are not the same, and the source can't send traffic directly to the destination.

.. note::

        Direct communication is only possible between devices on the same network.

.. _unit4_default_gateway:

Default Gateway
===============

Routers are the devices that connect different networks together. Default gateway is a router interface responsible for taking traffic off the network destined for other networks and bringing traffic from other networks back onto the network.

When a network device is configured either statically or dynamically, in addition to an :ref:`unit4_ip` and a :ref:`unit4_subnet_mask`, that device also gets an :ref:`unit4_ip` of a router interface on the network (Default gateway).

The source needs to get the traffic to its default gateway. Even though host A, the source, determines that the traffic is remote, it will once again send an :ref:`ARP request <unit4_arp>`, which is broadcasted to all devices on its network. This time, the :ref:`ARP request <unit4_arp>` is looking for the :ref:`unit4_mac` of host A's default gateway.

The gateway will send its :ref:`unit4_mac` in a unicast ARP reply back to host A. **Host A sends the traffic with a destination MAC adress of the router and the destination IP adress of the actual destination.**

.. note::

        Router interfaces hear broadcasts on the networks they're connected to but will never forward broadcast traffic from one network out of another interface to a different network.

Each interconnection between router interfaces, including the router interfaces themselves, is considered a separate network. Every device between router A's right interface and router B's left interface, including those interfaces, is on that shared network. The network identifier would be 10.10.2.0 if the subnet mask was 255.255.255.0. All devices on that network would need an :ref:`unit4_ip` starting off with 10.10.2. The last octet would be the host octet.

.. sourcecode::

         Host A       Host B                                                                            Host X
        10.10.1.1    10.10.1.2                                                                         10.10.4.1
            \          /                                                                                   |
             \        /             ┌                ┐              ┌                ┐              ┌      |
               Switch               |                |              |                |              |      |
                 |                  | Shared Network |              | Shared Network |              |      |
                 └------ Router A --|   10.10.2.x    |-- Router B --|   10.10.3.x    |-- Router C --| 10.10.4.x
                   10.10.1.99       |                |              |                |              |
                                    └                ┘              └                ┘              └ 
                                       
              10.10.1.0                 10.10.2.0                       10.10.3.0                      10.10.4.0
            255.255.255.0             255.255.255.0                   255.255.255.0                  255.255.255.0


.. _unit4_packets_routing:

Packet Routing
--------------

.. _unit4_routing_tables:

Routing tables
==============

Routers maintain tables called, routing tables that contain destination networks and directions for the router, who to send the traffic to next.

.. _unit4_icmp:

If the routers routing table doesn't have knowledge of the destination network, it can have a default route which means a specific router interface on a different router to send traffic to. Without knowledge of the destination network or a default route, a router will drop a packet and send an error message back to the source through a protocol known as **ICMP, Internet control message protocol**.

Host A's :ref:`unit4_default_gateway` looks in its routing table and sees that the next router interface the packet should go to is the left interface of Router B. If the routers are connected by the Ethernet infrastructure, the same :ref:`ARP process <unit4_arp>` takes place. If the interconnection between routers doesn't use Ethernet, a different `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ type is used.

Router A routing table:

============  ========================
Network       Next Hop IP address     
============  ========================
10.10.1.0/24  Directly connected Left  
10.10.2.0/24  Directly connected Right 
10.10.3.0/24  10.10.2.99               
10.10.4.0/24  10.10.2.99               
============  ========================

Router A sends an :ref:`ARP request <unit4_arp>`, a broadcast heard and read by every device on the network, looking for :ref:`unit4_ip` 10.10.2.99, send me your :ref:`unit4_mac`. The left interface of Router B sends a unicast :ref:`ARP reply <unit4_arp>` back to R1 with its :ref:`unit4_mac`.

Router A re-encapsulates the original packet sent from Host A to Host X with a new `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_. The new source :ref:`unit4_mac` represents the right interface of Router A, and the new destination :ref:`unit4_mac` represents the left interface of Router B.

Router B accepts the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ on its left interface, sees that the :ref:`unit4_mac` is its :ref:`unit4_mac`, then Router B inspects the destination :ref:`unit4_ip` and it isn't its :ref:`unit4_ip`. Router B's right interface then ARPs looking for the :ref:`unit4_mac` of Router C's left interface.

After the ARP reply comes back, the new source MAC of the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ is the right interface of Router B. And the new destination MAC is the left interface of Router C. Then Router C's right interface finishes it off by actually ARPing for the destination since the right interface of R3 is actually on the destination's network.

The final `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ has a source :ref:`unit4_mac` of the right interface of Router C and a destination :ref:`unit4_mac` of the actual destination, Host X. The destination gets the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_, sees its :ref:`unit4_mac`, opens it up, and confirms :ref:`unit4_ip`.

The IP header is now stripped off and the higher layer data is sent up the networking stack on the destination for processing.


MAC and IP Addresses Used Together
==================================

:ref:`MAC addresses <unit4_mac>` are only locally significant and are definitely needed in addition to :ref:`unit4_ip` to specify the next hop to receive the packet and route to its final destination.

Every time a packet passes through an interface, the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ is stripped off and discarded and after the next router figures out the next hop, the packet is reframed with a new outer `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_.

Binding IP Addresses to MAC Addresses
=====================================

:ref:`MAC addresses <unit4_mac>` alone wouldn't be enough for network communications. They are not hierarchical, but rather flat addresses.

:ref:`IP addresses <unit4_ip>` alone wouldn't be enough for network communications either. These logical addresses are leased to client devices on a dynamic basis. In most cases, they're even geographical with :ref:`unit4_ip` numbers representing different parts of the world.

The logical :ref:`unit4_ip` can be bound to and associated with a device as :ref:`unit4_mac` for a duration of time. That's how we keep track of which device is temporarily using an :ref:`unit4_ip` of a network at any point in time.

An :ref:`unit4_ip`, a :ref:`unit4_mac`, you simply can't have one without the other.
