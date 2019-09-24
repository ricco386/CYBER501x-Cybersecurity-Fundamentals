.. _unit7:

Unit 7 - Detection and Prevention
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _unit7_firewalls:

Firewalls
---------

Firewalls can be physical hardware devices, or simply software. Firewalls filter traffic based on rules. Filtering as far as firewalls are concerned means that certain packets are not let into a network.
It also means that packets on the way out of a network can be blocked from leaving. Certain packets will not be filtered. **Firewalls permit or deny traffic both inbound and outbound.**

Firewalls can filter by source :ref:`IP addresses <unit4_ip>`, destination :ref:`IP addresses <unit4_ip>`, protocols, ports, and other criteria.

* Hardware based firewalls are also referred to as network based firewalls.
* Software based firewalls are also known as host based firewalls.

.. _unit7_stateless_packet_filtering:

Stateless packet filtering
==========================

Stateless packet filtering, which is sessionless. Each packet is treated by itself as an isolated piece of communication. This requires less memory and time. There's low overhead and high throughput. However, this type of firewall technique cannot make complex decisions based on a communication stage.

.. _unit7_stateful_packet_filtering:

Stateful packet filtering
=========================

Stateful packet filtering, uses sessions, can understand stages of a TCP connection, and can be aware of a hacker who tries to spoof an :ref:`IP address <unit4_ip>`.

.. _unit7_alg:

An ALG, application layer gateway, applies security mechanisms based on a certain application, like HTTP, SSL/TLS, FTP, DNS, and VoIP.

So instead of just looking at :ref:`IP addresses <unit4_ip>`, protocols, and ports, ALG's look deeper into the protocols to see if they're being used properly. ALG's understand how specific protocols should work and look at layer seven. They can filter offensive or disallowed commands in the data stream. They are stateful.


.. _unit7_dpi:

DPI - Deep packet inspection
----------------------------

DPI, deep packet inspection, is done by an :ref:`ALG <unit7_alg>` to examine in great detail the contents of the data being sent.


.. _unit7_dci:

DCI - Deep content inspection
-----------------------------

:ref:`DPI <unit7_dpi>` has actually evolved into DCI, deep content inspection, which examines an entire file. DCI puts together parts of actual objects that are transmitted in parts of different packets, like PDF's and images. DCI even decodes and decompresses files. This is a much greater form of intelligence than partial data `layer seven <https://en.wikipedia.org/wiki/Application_layer>`_ that :ref:`DPI's <unit7_dpi>` deal with.


.. _unit7_ids:

IDS - Intrusion detection system 
--------------------------------

IDS is out of band, and simply gets copies of network traffic. It can be as simple as a system getting copies of traffic to inspect through a switch configured to send all traffic to the IDS.

Since the IDS is out-of-band, it doesn't add any latency. If the IDS sensor goes down, possibly after a target attack, traffic will still flow. An IDS can alert an administrator and even automatically tell a firewall to block traffic based on what it observes.


.. _unit7_ips:

IPS - Intrusion prevention system
---------------------------------

IPS is in-line, so original traffic must pass through the IPS. An IPS adds latency, since traffic is processed live.

If an IPS is targeted, attacked, brought down, traffic might stop right there. An IPS can alert an administrator and even automatically tell a firewall to block traffic based on what it observes.

Both :ref:`IDSs <unit7_ids>` and IPSs are vulnerable to false-positives. The latest anomaly-based :ref:`IDSs <unit7_ids>` and IPSs can detect malicious insiders as well as machines or accounts that have been compromised from outsiders.


.. _unit7_honeypots:

Honeypots and Deception Software
--------------------------------

Honeypot is a computer with intentionaly broken security to attract attackers. Typically these honeypots encourage attackers to stay on the system long enough for administrators to document and respond to the attack. It also allows administrators to refine the firewall rules based on observed attacker behaviors.

.. _unit7_deception_software:

**Deception software is the new wave of honeypots.** These decoys can be centrally managed, made to work with other security software, and run through virtualization. Intruders can be fooled at many layers, such as network; endpoint; application; and data with fake browser credentials and decoy work stations; phony files; datasets; and more.

.. _unit7_social_engineering:

Social engineering
------------------

Social engineering involves preying on humans who are gullible and naive, and will always be the weakest link in cybersecurity system. Social engineering has been described as the art and science of getting people to comply to your wishes and an outside hacker's use of psychological tricks on legitimate users of a computer system.

In order to obtain information, he needs to gain access to the system. Social engineering is when a hacker tricks someone into doing something they normally wouldn't and shouldn't do from a cybersecurity perspective.
