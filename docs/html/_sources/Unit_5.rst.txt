.. _unit5:

Unit 5 - Networking 2
~~~~~~~~~~~~~~~~~~~~~

The way network communication goes in and out of a machine physically is through the NIC, network interface card. The way network communication goes in and out of a machine logically, though, is through a program or service. **A service is a program that runs in the background, independent of a log on that provides functionalities to a system.** When you start a web server, you're starting a specific server service that isn't tied to a specific user log on either. This way, when the server reboots, the service automatically starts before anyone logs on. In the world of Linux, services are known as daemons.

.. _unit5_ports:

Ports
-----

Multiple services are running on the same host (they have the same :ref:`unit4_ip`), traffic for each service is determined by the the service port. **A port is a logical end point of communication that identifies a program or service and is represented by a port number.** So in addition to source and destination :ref:`MAC addresses <unit4_mac>` and source and destination :ref:`IP addresses <unit4_ip>`, there are, source and destination ports.

Mac addresses are found in `frames <https://en.wikipedia.org/wiki/Frame_(networking)>`_ at layer two of the `OSI model <https://en.wikipedia.org/wiki/OSI_model>`_. :ref:`IP addresses <unit4_ip>` are found in packets at layer three. Port numbers are found in either :ref:`TCP <unit5_tcp>` segments or :ref:`UDP <unit5_udp>` datagrams at `layer four <https://en.wikipedia.org/wiki/Transport_layer>`_. Based on the destination port, the destination machine knows which program or service to send the data.

* Well-known ports from zero to 1,023 are used by major protocols and services.
* Registered ports from 1,024 to 49,151 are assigned by IANA, the Internet Assigned Numbers Authority, for specific companies that want a common port to be used for their programs or protocols.
* Dynamic ports from 49,152 to 65,535 are used by client applications on an as-needed basis.

For example, your browser might open up port 60,000 to send a request to a web server that will be listening for requests on port 80, unencrypted HTTP. The web server's response is sourced from port 80 and is destined for the port that your browser opened up. After the communication between your browser and the web server is complete, your browser will close the port it opened. But the web server's port will remain open for new incoming connections.

One of two protocols will be used at `Layer 4 <https://en.wikipedia.org/wiki/Transport_layer>`_ of the `OSI model <https://en.wikipedia.org/wiki/OSI_model>`_ to encapsulate the data coming from `Layers 5 <https://en.wikipedia.org/wiki/Session_layer>`_, `6 <https://en.wikipedia.org/wiki/Presentation_layer>`_, and `7 <https://en.wikipedia.org/wiki/Application_layer>`_.

:ref:`TCP <unit5_tcp>`, Transmission Control Protocol segments, or :ref:`UDP <unit5_udp>`, User Datagram Protocol datagrams, will be selected by an application that's sending data.

.. _unit5_tcp:

TCP - Transmission Control Protocol 
-----------------------------------

TCP establishes a connection between the source and destination devices for reliable data transfer and flow control, sending data at an acceptable rate, both to the source and destination.

.. note::
	
	TCP guarantees that every single byte sent will be received with integrity and processed in the correct order.

TCP segments are acknowledged. So the sender knows the destination got the traffic. If an acknowledgment specifically referencing byte numbers of the data sent doesn't come back, TCP resends the unacknowledged bytes.

TCP is used for things like file transfers, email, and going to websites. In those cases, accuracy is important. If bytes are lost or corrupted, the whole message could be destroyed.

.. _unit5_udp:

UDP - User Datagram Protocol
----------------------------

UDP is connectionless and has no flow control. All bytes sent with TCP are ordered and sequenced.

UDP is used for real-time communications, conferencing and streaming. Furthermore, two major protocols :ref:`DNS <unit6_dns>` and :ref:`DHCP <unit6_dhcp>`, both use UDP.

.. _unit5_rstp:

RTSP - Real Time Streaming Protocol
-----------------------------------

RSTP which exists at `Layer 7 <https://en.wikipedia.org/wiki/Application_layer>`_, does the ordering of the packets for :ref:`UDP <unit5_udp>`. Using RTSP just for the ordering of the :ref:`UDP <unit5_udp>` datagrams involves significantly less overhead than :ref:`TCP <unit5_tcp>` would require.

.. note::

	:ref:`TCP <unit5_tcp>` has much more overhead than :ref:`UDP <unit5_udp>` and is deliberately slower, striving for accuracy and integrity. :ref:`UDP <unit5_udp>` has no overhead, and it's quicker, striving for efficiency.

.. _unit5_switches:

How Switches Work
-----------------

Switches connect devices of the same network together. They can connect into other switches and routers as well. Switches and PCs connected between router interfaces are considered to be on the same network.

When a PC sends an Ethernet `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ into a switch, the switch checks the destination :ref:`unit4_mac` to see if it knows which interface that :ref:`unit4_mac` is connected to. If the switch knows where the device with that :ref:`unit4_mac` is, the switch sends it out, just that interface. If the switch doesn't know where a destination :ref:`unit4_mac` is, the switch floods the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ out of all interfaces except the interface on which the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ originated.

The switch actually starts off knowing nothing, but as `frames <https://en.wikipedia.org/wiki/Frame_(networking)>`_ are sent into the switch, the switch starts learning. If host A sends a `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ for host B into the interface on the switch, the switch says I know that the :ref:`unit4_mac` of host A can now be associated with the interface on which it was heard. **The switch will make a note of it through a table in memory called SAT, Source Address Table.**

Since the switch doesn't know where host B is, it floods the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ out of all the interfaces except the one the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ originated on. When host B replies, the `frame <https://en.wikipedia.org/wiki/Frame_(networking)>`_ goes into the switch. And the switch learns that host B's interface. The switch then adds the :ref:`unit4_mac` of host B and the interface it was heard on into its source address table as well. The logic works the same for switches that are connected together.

If there are 20 connected switches in a network with 20 PCs connected to each of those switches, a single :ref:`ARP request <unit4_arp>` by one of the PCs will be read by the other 399.

.. _unit5_autonomous_systems:

Autonomous Systems
------------------

Routers don't connect devices of the same network together. They connect different networks together. So you wouldn't ever see a PC connected to a router.

If the router has no knowledge of the destination network, it might have a default route of its own to send the packet to. Without either knowledge of a destination network or a default route for a router to send all packets with unknown destinations to, the router will drop the packet, and send an error message back to the source through a protocol known as **ICMP, Internet control message protocol**.

**An autonomous system represents a collection of networks under one administrative control, like an ISP or major entity like RIT.**

Why would a bunch of networks be preferred to a single network?

* :ref:`ARP requests <unit4_arp>` and all other broadcast traffic will always reach and be processed by every single device on a network. One reason why we might want multiple networks interconnected by routers instead of one big flat network is to reduce the size of the broadcast domain.
* For security purposes multiple networks are preferred to one big flat network. Security at the router level in the form of an access control list can be used to filter traffic by source :ref:`unit4_ip`, destination :ref:`unit4_ip`, protocols, and even :ref:`ports <unit5_ports>`. This allows you to control access to and from certain devices and resources much better than if everything was on the same network.
* The troubleshooting process is easier by isolating traffic to a certain network.

.. _unit5_dynamic_routing:

Dynamic Routing
===============

Entities like RIT registered for and received their own **ASN, Autonomous System Number**. They became autonomous systems of their own, independent of ISPs. This allowed them to maintain routing tables and exchange routing information with multiple ISPs. As traffic is ready to leave the autonomous system, the routers decide which ISP and which ISP connection to send the traffic to for the most efficient packet delivery.

Inside a company, within an autonomous system, there needs to be a dynamic way in which the routers can exchange information about the internal networks as well as how to get to the company's edge router that connects to the ISP for packets destined for an external network. This is where **routing protocols** come into play:

.. _unit5_igp:

IGP - Interior Gateway protocol
-------------------------------

An IGP is a routing protocol that allows routers within an autonomous system to communicate with each other. Sharing information about the networks they're directly or indirectly connected to. After these messages are passed between the routers, each router forms an idea of the topology and determines the best way to get to it a destination network.

Metrics are values that the routers use to determine the best way to get to a destination network when there are multiple paths available.

.. _unit5_ospf:

OSPF - Open Shortest Path First
===============================

.. _unit5_eigrp:

EIGRP - Enhanced Interior Gateway Routing Protocol
==================================================

The main metric used by OSPF and EIGRP to determine the best way to get to a destination network is bandwidth although they calculate this metric very differently.

Using OSPF or EIGRP, a router might choose a path to a destination network with more hops over a path with fewer hops based on the bandwidth. Sending a packet over a greater number of links is preferred if those links and their bandwidth can get the packet to its destination quicker than a smaller number of links.

.. _unit5_egp:

EGP - Exterior Gateway Protocol
-------------------------------

An EGP is a routing protocol that allows routers from different autonomous systems to communicate with each other and exchange routing information.

.. _unit5_bgp:

BGP - Border Gateway Protocol
=============================

The only EGP in usage today, which is used across the entire Internet, is BGP.
