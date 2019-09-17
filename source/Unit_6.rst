.. _unit6:

Unit 6 - Systems Administration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Back in the early days of networking, devices were statically, manually configured with their 32-bit IPv4 addresses and subnet masks. This is not scalable, and also prone to human errors.

.. _unit6_rarp:

RARP - Reverse Address Resolution Protocol
------------------------------------------

RARP is reverse :ref:`ARP <unit4_arp>`. A diskless work station would still have a NIC, and therefore a :ref:`unit4_mac`, and would ask a Reverse ARP server for an :ref:`unit4_ip`.

Administrators would pre-configure a table on the Revers ARP server matching :ref:`Mac addresses <unit4_mac>` of devices to the :ref:`IP addresses <unit4_ip>` that would be dynamically handed out to them upon request. 
:ref:`ARP <unit4_arp>` matches an :ref:`unit4_ip` to a corresponding :ref:`unit4_mac`. **Reverse ARP matches a :ref:`unit4_mac` to a corresponding :ref:`unit4_ip`, hence the term "Reverse ARP".**

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

Relay agents were router interfaces on a network, also serving as the full gateways, that took broadcast BootP messages and turned them into unicast messages, relaying them through the normal IP routing process to the prepare BootP servers. 
The BootP servers sent responses back to the relay agents, who relayed those messages back to the clients. This way, you can have two BootP server on a single network giving out :ref:`IP addresses <unit4_ip>` for many other networks.

.. _unit6_dhcp:

DHCP - Dynamic Host Configuration Protocol
------------------------------------------

DHCP's improvement over :ref:`BootP <unit6_bootp>` was something called scopes, which are ranges of :ref:`IP addresses <unit4_ip>` that are used in a dynamic fashion.
A client machine asks the DHCP server for an :ref:`unit4_ip` and if there are addresses left in this dynamic pool, the server picks one and assigns it to the host, binding the logical :ref:`unit4_ip` to the host's physical 
:ref:`unit4_mac` for a duration of time. This concept is known as a lease.

DHCP was made to be an extension of :ref:`BootP <unit6_bootp>` because of :ref:`BootP's <unit6_bootp>` capability of :ref:`relay agents <unit6_relay_agents>`. DHCP was made to be an extension of BootP so that relay agents would be able
to relay either BootP or the new DHCP messages. Option 53 distinguishes DHCP from :ref:`BootP <unit6_bootp>` in the `Layer 7 <https://en.wikipedia.org/wiki/Application_layer>`_ fields.

.. _unit6_dns:

DNS - Domain Name System
------------------------