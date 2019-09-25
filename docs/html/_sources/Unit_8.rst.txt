.. _unit8:

Unit 8 - Malware and Forensics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _unit8_malware:

Malware, short for malicious software, is intended to damage or break a computer system or network without user knowledge or approval. There are many different types of malware but the two most often confused ones are viruses, worms and other types of malicious software.

.. _unit8_virus:

Virus 
-----

Virus injects itself into a program's instructions, so that the CPU will execute the malicious instructions when they are reached in the original program. Just like a biological virus, a computer virus needs a host file to infect and that file has to be run for the virus to start running. The infected host file, in addition to a program, could be a data file or even the boot sector of a hard drive. The malicious instructions, whenever read, are executed by the CPU.

Viruses can spread and replicate by themselves to other files on the same machine. But in order to spread and replicate to other machines on the network and other networks across the world, some human intervention is required.

Viruses always have malicious payload that is meant to execute.

.. _unit8_worm:

Worm
----

Worm does not infect host files. It stands alone in its own file.

Worms can propagate all by themselves across networks all around the world. They exploit vulnerabilities in protocols, networks, and configurations.

.. _unit8_ddos:

Worms don't need to have any malicious payload. Infected machines, known as zombies in this botnet, robot network, will be instructed to do something. Likely sending traffic to a server that will come to a grinding halt. This common attack is known as a DDoS, distributed denial of serve attack.

.. note::

Interestingly enough, a DDoS doesn't go after the confidentiality or integrity of the CIA model. It's meant to go after the A, the availability of a system or a network.

.. _unit8_logic_bomb:

Logic bomb
----------

A logic bomb is another introduces latency to when it executes. Either a certain date, time, or event will trigger this type of malware to run.

From a malware author's perspective, the longer amount of time that goes by before a new malware specimen is detected, the better. This allows the malware to spread and remain silent so antivirus companies don't pick up on it. Then after a period of time, the malware on all infected systems will run.

.. _unit8_rat:

RAT - Remote Access Trojan
--------------------------

A RAT, remote administration tool, is a piece of software used to remotely access or control a computer. This tool can be used legitimately by administrators systems for accessing client computers or servers.

A RAT, when used for malicious purposes, is known as a remote access Trojan. It can be used by a malicious user to control a system without the knowledge of users of that system. Remote access Trojans are malicious pieces of software that infect victim machines to gain administrative access.

They are often included in pirated software through patches as a form of a cracked game or even via email attachments. Most of the popular RATs are capable of performing keystroke logging, packet capture, screen capture, camera capture, file access, code execution, registry management, password sniffing, and more. After the infection, they may perform unauthorized operations and hide their presence in the infected system.

.. _unit8_rootkit:

Rootkit
-------

Rootkit, is a set of programs and code that allows a persistent or permanent undetectable presence on a computer.

A rootkit can sanitize logs and repair timestamps, hiding actions of the hackers. A rootkit can also mask files, processes, and network connections and enable privileged access to the computer. It also conceals installed malware. Rootkits also install another piece of malware called a backdoor.

.. _unit8_backdoor:

Backdoor
--------

After hackers exploit vulnerabilities to get into your system or network, they want to come back later with less effort. Backdoors allow hackers to do so, bypassing the normal authentication process through software left after the initial penetration.

.. _unit8_spyware:

Spyware
-------

Spyware covertly monitors user's activities and reports personal user data to a third party that expects financial gain.

Spyware also includes the sale of personal data, the redirecting of web activity to ad sites, and the presentation of targeted ads and pop-ups through a related piece of malware called adware.

.. _unit8_adware:

Adware
------

Adware automatically plays or displays advertisements or downloads promotional material.

It's often bundled with a product or package and it's common in shareware, free software that might require subsequent payment after a trial run.

.. _unit8_pup:

PUP - potentially unwanted program
----------------------------------

Once Spyware or Adware is listed in EULA to avoid any legal issues, the term PUP, potentially unwanted program, was invented as a lesser way of saying Trojan horse.

.. _unit8_phishing:

Phishing
--------

Phishing involves sending out bait mostly through email to a large number of people.

Hoping some users will bite by sending usernames, passwords and even credit card information. When clicking a link in a phishing email the user is brought to a webpage that looks and feels like a real site. Therefore the user feels safe and secure in entering sensitive information, which goes directly to the attacker. Furthermore simply visiting these sites could install malware on a victim machine.

.. _unit8_spearphishing:

Spearphishing
-------------

Spear phishing takes phishing to a whole new level by targeting specific users of a specific company. Instead of just random email addresses that may or may not be valid.

.. _unit8_whaling:

Whaling
-------

When you go after the big fish of a company, like anyone that has a title beginning with a C and ending with an O, that's taking spear phishing to a whole new level and is called whaling.

.. _unit8_pharming:

Pharming
--------

Farming is the hijacking of a legitimate website's IP address and or domain name. It redirects unsuspecting users to a fake site and collects information that users enter like passwords, banking information and other PII (Personal Identifiable Information).

.. _unit8_watering_hole:

Watering Hole
-------------

A watering hole is a computer attack strategy in which the victim is in a particular group. Whether it's an organization, an industry or a region. In this attack the hacker guesses or observes which websites the group often uses and then the hacker infects one or more of those sites with malware. Eventually some member of the targeted group gets infected. Relying on websites that the group trusts makes the strategy efficient. Even with groups that are resistant to the different forms of phishing.

.. _unit8_ransomware:

Ransomware
----------

Ransomware, which locks and encrypts a device until ransom fee is paid. Scare tactics include threatening the users that if they don't pay by a certain amount of time, files will start to be deleted. The general recommendation is not to pay the ransom.

The best way to be safe is to not click on any unknown links and to keep a good set of backups that you can bring back and restore from, instead of paying the ransom fee.

.. _unit8_digital_forensics:

Digital Forensics
-----------------

Forensic science uses scientific and mathematical processes to analyze physical evidence. This evidence can be used to inculpate, prove that somebody did something, or exculpate, prove that someone didn't do something, in both civil and criminal cases.

Digital forensics is a subcategory of forensic science. It deals with the acquiring and investigating of material found in digital devices, often in relation to computer crime. Computer forensics is a subcategory of digital forensics. There are other subcategories of digital forensics, like network forensics, and mobile device forensics.

Digital forensics has also a major purpose, to figure out what happened in a cyber security related attack.

Forensic readiness adds value to your cybersecurity process. Evidence for a company's defense can be gathered with minimal disruption to the business.

There are a few different ways computing devices can be part of a forensic investigation:

* First, computing devices can be the tool used to commit a crime.
* Secondly, when a computing device is hacked, it is the target of a crime.
* Thirdly, storage locations on a computing device represent repositories for evidence of a crime.

.. _unit8_incident:

Cybersecurity incident
======================

A cybersecurity incident is any illegal, unauthorized, or unacceptable action that involves a computing system or network. Incidents are breaches of cybersecurity measures that were put in place before.

.. _unit8_incident_response:

Incident response
=================

Incident response is the forensic examination of systems and networks after they have been attacked. It also involves taking actions to remediate an ongoing incident, like blocking the attackers and restoring any lost availability as quickly as possible.

.. _unit8_cybercrime:

Cybercrime
==========

Cybercrime is any illegal activity involving a computing device, its systems, or its applications.

.. _unit8_digital_evidence:

Digital Evidence
----------------

It's information stored or transmitted in binary form that may be relied on in court and it's comprised of both data and metadata.

This could include contact information; evidence of malicious attacks on systems; GPS location and movement records; transmission records, both authorized and unauthorized; system use or abuse; account production and use, either authorized or unauthorized; correspondence records; and content like images and files.

This evidence can potentially answer common questions: Who? What? Where? When? How? Why?

Different cyber crimes result in different types of digital evidence. Computer hackers may leave evidence of their activities in log files. Cyber stalkers use email to harass their victims. etc...

Host-based information on computing devices can include both volatile data stored in RAM which is lost when there's no power, and non-volatile data on the hard drive which stays when there's no power. Optical discs and removal devices could also contain artifacts and remnants of significance for the investigator.

.. _unit8_forensics_investigations:

Forensics Investigations
------------------------

1. Evidence is acquired and imaged.
2. The evidence is analyzed.
3. Report is made, which should be understandable to even non-technical individuals.

Gather Image
============

A forensic investigator needs to choose the way to acquire evidence that minimizes data loss, gather all the pertinent evidence, maintain the integrity of originals, create copies, and always work on the copies.

Avoid destroying volatile data, missing critical data, altering timestamps, using untrusted commands or allowed tools, or adjusting the system prior to evidence seizure through patching or updating. Digital evidence must be preserved in its original state. The law requires that evidence be authentic and unaltered to be admissible in a court of law.

.. _unit8_hash_functions:

**Hash functions are used to positively verify that a file or entire hard drive hasn't been altered.** And also to verify that files, hard drives, and their copies are intact, and have not changed during the investigation.

.. _unit8_bitstream_copy:

Making a **bitstream copy means to image a hard drive bit-for-bit from all sectors**. It is performed on the hard drive level, not the file system level. It copies metadata and data blocs in their entirety, regardless of whether they're allocated to an active file or not. It also copies slack space.

Hard drives store files in clusters of a certain size. Slack space represents the location of the end of a file on a hard drive to the end of the file cluster that the file is stored in. In this slack space, a forensic investigator can find deleted files, or at least fragments of deleted files and hidden data.

Evidence can also be found in unallocated space. When you delete a file, the operating system marks that location as available, but the file that was deleted from the file system is still there in the unallocated space until the operating system chooses to use that location for a new file.

Analysis
========

In a cybersecurity-related forensic investigation, the analysis phase can confirm or dispel the existence of an incident.

Report
======

The step-by-step procedures of the imaging, details of each test, the tools used, and the facts uncovered should be written in a non-technical form so attorneys, the judge, and jury can all understand what the investigator is testifying to.

This preservation process, known as the chain of custody, occurs throughout an entire investigation, from acquisition of evidence through the time the investigator testifies as an expert witness in a court of law. The chain of custody is used to maintain a record of how evidence has been handled from the moment it was collected to the moment it was presented in court.

.. _unit8_anti-forensics:

Anti-forensics 
--------------

Anti-forensics is designed to thwart discovery of information related to illegal activities of a user.

A suspect might manipulate, erase, or obfuscate digital data to make its examination difficult, time consuming, or virtually impossible. Data-hiding techniques include obfuscating data by encryption or compression. Data could also be hidden through codes, giving innocent-looking data an alternate meaning.

One way this is done is through a process known as steganography, which hides files and data inside of other files. Files could also be hidden with misleading file names or extensions, but this won't fool forensic tools. The tools look at the first few bytes of a file, and based on these well-known signatures, the tools will identify what type of file it is, regardless of an extension.
