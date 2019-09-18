.. _unit6:

Unit 6 - Systems Administration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Back in the early days of networking, devices were statically, manually configured with their 32-bit IPv4 addresses and subnet masks. This is not scalable, and also prone to human errors.

.. _unit6_rarp:

RARP - Reverse Address Resolution Protocol
------------------------------------------

RARP is reverse :ref:`ARP <unit4_arp>`. A diskless work station would still have a NIC, and therefore a :ref:`unit4_mac`, and would ask a Reverse ARP server for an :ref:`unit4_ip`.

Administrators would pre-configure a table on the Revers ARP server matching :ref:`Mac addresses <unit4_mac>` of devices to the :ref:`IP addresses <unit4_ip>` that would be dynamically handed out to them upon request. 
:ref:`ARP <unit4_arp>` matches an :ref:`unit4_ip` to a corresponding :ref:`unit4_mac`. **Reverse ARP matches a** :ref:`unit4_mac` **to a corresponding** :ref:`unit4_ip` **, hence the term "Reverse ARP".**

However, the :ref:`Mac addresses <unit4_mac>` still needed to be collected and entered along with the :ref:`unit4_ip` that would be handed out on the Reverse ARP server.

Another problem with Reverse ARP was that like :ref:`ARP <unit4_arp>`, it was a layer to protocol that existed inside of `frames <https://en.wikipedia.org/wiki/Frame_(networking)>`_. Since there was no IP header, it couldn't be sent off a network. 
What that meant was that each and every network needed its own Reverse ARP server.

.. _unit6_bootp:

BootP - Bootstrap particle
--------------------------

BootP messages were encapsulated in UVP data grams at `Layer 4 <https://en.wikipedia.org/wiki/Transport_layer>`_, which were encapsulated in IP packets at `Layer 3 <https://en.wikipedia.org/wiki/Network_layer>`_.
This way messages could actually by routed off a network and the need for a server on each and every network was eliminated (unlike in :ref:`RARP <unit6_rarp>`).

A machine would boot up, send a request to the BootP server with its :ref:`unit4_mac`, and it would be assigned an :ref:`unit4_ip` that the admin chose for that :ref:`unit4_mac`. Relay agents made this possible.
Routers don't forward broadcasts, but part of the BootP sequence involved broadcasting a request to a BootP server, because obviously the client doesn't have any knowledge of anything at that point in time.

.. _unit6_relay_agents:

**Relay agents** were router interfaces on a network, also serving as the full gateways, that took broadcast BootP messages and turned them into unicast messages, relaying them through the normal IP routing process to the prepare BootP servers. 
The BootP servers sent responses back to the relay agents, who relayed those messages back to the clients. This way, you can have two BootP server on a single network giving out :ref:`IP addresses <unit4_ip>` for many other networks.

.. _unit6_dhcp:

DHCP - Dynamic Host Configuration Protocol
------------------------------------------

DHCP's improvement over :ref:`BootP <unit6_bootp>` was something called scopes, which are ranges of :ref:`IP addresses <unit4_ip>` that are used in a dynamic fashion.
A client machine asks the DHCP server for an :ref:`unit4_ip` and if there are addresses left in this dynamic pool, the server picks one and assigns it to the host, binding the logical :ref:`unit4_ip` to the host's physical 
:ref:`unit4_mac` for a duration of time. This concept is known as a lease.

DHCP was made to be an extension of :ref:`BootP <unit6_bootp>` because of :ref:`BootP's <unit6_bootp>` capability of :ref:`relay agents <unit6_relay_agents>`. DHCP was made to be an extension of BootP so that relay agents would be able
to relay either BootP or the new DHCP messages. Option 53 distinguishes DHCP from :ref:`BootP <unit6_bootp>` in the `Layer 7 <https://en.wikipedia.org/wiki/Application_layer>`_ fields.

.. _unit6_dhcp_dora:

DHCP's DORA
===========

The general process of a client requesting and getting an IP address from a :ref:`DHCP <unit6_dhcp>` server is DORA, which is an acronym for four specific DHCP message types:

* Discover
* Offer
* Request
* ACK, short for Acknowledge

A client device will broadcast a :ref:`DHCP <unit6_dhcp>` discover message at both `Layer 2 <https://en.wikipedia.org/wiki/Data_link_layer>`_ and `Layer 3 <https://en.wikipedia.org/wiki/Network_layer>`_. 

* The `Layer 3 <https://en.wikipedia.org/wiki/Network_layer>`_ broadcast address is 255.255.255.255. 
* The `Layer 2 <https://en.wikipedia.org/wiki/Data_link_layer>`_ broadcast addresses 12 F's.

For the source :ref:`unit4_ip`, the client uses the unspecified address of 0000, quad 0. The client's :ref:`unit4_default_gateway`, also acting as its :ref:`relay agent <unit6_relay_agents>`, will need to be pre-configured to know about 
the :ref:`DHCP <unit6_dhcp>` servers in the autonomous system. When this router interface sees the broadcast traffic and inspects the UDP datagram to see a DHCP discover message, the router will replace both the frame and the packet 
and send the UDP datagram as a unicast message in a new frame and packet to a DHCP server through the normal routing process. The server, when it gets the DHCP discover, which is now a unicast, will check to see the relay agent's IP address, which 
was added to the DHCP portion of the message. This allows the DHCP server to know which network the client is on and give the client an address accordingly.

.. sourcecode::

	┌------------------------------------------------------------┐
	|           ┌-----------------------------------------------┐|
	|           |              ┌-------------------------------┐||
	|           |              |              ┌---------------┐|||	
	|  Frame 2  | IP Header2   | UDP Header   | DHCP Discover ||||
	|           |              |              └---------------┘|||
	|           |              └-------------------------------┘||
	|           └-----------------------------------------------┘|
	└------------------------------------------------------------┘

The gateway will always be on the same network as the client, assuming a subnet mask for all networks of 255.255.0.0, which means the first two octets are networked octets and the last two octets are host octets.

* If the router's IP address 10.1.0.99, the DHCP server will give the client an IP address that starts with 10.1.
* If the router's IP address 10.2.0.99, the DHCP server will give the client an IP address that starts with 10.2.

Each subnet has its own scope on the DHCP server. Based on the IP address of the relay agent, the DHCP server knows which scope to select an IP address from. In a similar fashion, the DHCP client transmits its MAC address 
in the DHCP discover message. This allows the DHCP server to associate that MAC address with the IP address it leases to the DHCP client.

That's how the DHCP server knows which DHCP client is using an IP address at any point in time. The DHCP server will also give other pieces of information to the DHCP client, including subnet mask, default gateway IP address, 
DHCP server addresses, DNS server addresses, and more. The server sends a DHCP offer in a unicast message back to the relay agent, who relays it back to the client. Most dedicated DHCP servers will send this back as 
a unicast message to the client, with or without a relay agent, even though the client doesn't yet have true possession of the IP address.

.. _unit6_dhcp_ack:

After the client gets the DHCP ACK from the relay agent, the client will now be able to start sending unicast messages from this IP address.

.. _unit6_dns:

DNS - Domain Name System
------------------------