# **Security risk assessment report** 

**Scenario**

You are a security analyst working for a social media organization. The organization recently experienced a major data breach, which compromised the safety of their customers’ personal information, such as names and addresses. Your organization wants to implement strong network hardening practices that can be performed consistently to prevent attacks and breaches in the future. 

After inspecting the organization’s network, you discover four major vulnerabilities. The four vulnerabilities are as follows:

1. The organization’s employees' share passwords.  
2. The admin password for the database is set to the default.  
3. The firewalls do not have rules in place to filter traffic coming in and out of the network.  
4. Multifactor authentication (MFA) is not used. 

If no action is taken to address these vulnerabilities, the organization is at risk of experiencing another data breach or other attacks in the future. 

**Investigation**

**Password sharing culture**  
The investigation highlighted password sharing between employees on several key systems used by the organisation. Multiple instances of individuals within teams requesting logon credentials and sharing them amongst their team were identified, in violation of organisational policy which requires users to request individual personal logon credentials and to keep these private. In several team offices, these passwords are written on paper and prominently displayed. It is conceivable that those who have since left the organisation are still in possession of these passwords.

**Database default password**  
The password for the database containing personally identifiable information (PII) of customers has not been changed from the default password provided by the software provider. This password follows a well known format widely available on the internet and would have been easy for the attacker to guess. Instructions to change the password after the initial login have been ignored despite this appearing each time users log on.

**Firewall rules**  
Despite using an effective, commonly used and industry-respected stateful firewall software, the investigation highlighted that its various deployments across the network have received minimal configuration. Firewall default configuration settings have been changed little. Whilst some basic rules are in place to allow for key services to communicate over the network, rules skew heavily towards permissiveness and an “allow by default” philosophy for trusted IPs. In addition, there is currently no network segmentation, meaning that compromised trusted devices and attackers who have illicitly gained access to internal networks have a large degree of unimpeded access to internal systems. This is compounded by alert settings, which have not been changed from default settings and provide notifications only in the event of high-confidence attack patterns.

**Multi-factor authentication**  
The organisation is currently reliant on single factor password authentication. As above, password practices for crucial systems are poor and this is compounded by the absence of any additional authentication measures. Once a user uses a weak, shared password they have access to the system with no further verification and minimal restriction (see above firewall rules section). 

**Recommended measures in response to the attack**

**Passwords/authentication**

* **Staff training**. The investigation highlighted poor staff knowledge of security measures, the rationale behind them, and an entrenched culture of poor cyber security practice across the organisation. Extensive training to tackle this for all staff is recommended to combat this.  
* **Principle of least privilege.** A scoping exercise using the principle of least privilege is recommended to identify which users need access to specific systems, and to determine the level of access users need within a system based on their role.  
* **Automated policy enforcement measures**. At present there are password policies governing password length and necessary characters, however, if a user fails to meet this standard the system allows for the weak password to be used. Configuring a password police using Microsoft Active Directory to allow users only to use passwords which meet the specified standard is recommended.  
* **Multi-factor authentication** is recommended to ensure that even if a user’s password is compromised, an attacker is still unable to gain access. The organisation uses Microsoft Windows, which offers its own authenticator app that can be installed on mobile devices.

**Network segmentation and firewall settings**

* **Network segmentation**. The organisation currently employs around 5,000 employees. At present the network is not segmented and is reliant on firewall rules to allow or deny users access to systems. The segmentation of the network into different subnets is recommended, as well as the restriction of users to areas of their respective subnet(s) based on the principle of least privilege review recommended above.  
* **Review of current firewall policies**. Numerous unused reports were identified during the investigation. A full review of open ports will be needed, and those no longer required will need to be disabled.  
* **Firewall notification settings**. Default firewall settings set by the manufacturer are currently those used, these provide very few notifications and will require review inline with the firewall policies to ensure that network administrators are made aware in the event of a possible breach.

**Further measures**

**Encryption**

* The organisation currently uses the TLS 1.2 encryption standard to encrypt communication between endpoints on the network. TLS 1.3, a more secure replacement, is now widely adopted across organisations and it recommended that the organisation implement this newer and more secure standard.  
* The organisation currently uses the WPA2 encryption standard to encrypt communication between wireless access points and devices on the network. WPA3 is the more secure standard being adopted, and it is recommended that the organisation also implements this encryption standard to further secure the network. 

**Differences between WPA2 and WPA3 encryption**

The Wi-Fi Protected Access protocols, or WPA protocols, is a group of protocols designed to secure communication between wireless access points (APs) and devices on a local area network (LAN). WPA3 is the latest and most secure version and is the recommended security standard.

Upgrading network encryption from WPA2 to WPA3 is a one-off network hardening measure, providing considerable security benefits. The biggest benefit of changing to WPA3 is arguably that it addresses the key reinstallation attack (KRACK) vulnerability, replacing it with a new “handshake” known as simultaneous authentication of equals (SAE). Additionally, WPA3 offers other encryption benefits such as enhanced encryption of past recorded network traffic and open Wi-Fi networks, as well as higher 192-bit encryption for enterprise.

WPA3 resolves a security flaw present in both WPA2 and its predecessor, WPA1, known as a key reinstallation attack (KRACK). KRACK exploits a mechanism in the four-way handshake which the AP and client use to agree on an encryption key prior to data transmission.

	*What is the KRACK vulnerability?*  
To understand this vulnerability, it is first necessary to outline the key components used when an AP and client agree to transmit encrypted data on a network. Data encryption in WPA2 uses several numbers to generate unique encryption keys for data transmission:

* **Pairwise Master Key (PMK):** a code generated from the service set identifier (SSID) and the network password. This code remains the same until the network password is changed.

* **ANonce and SNonce**: numbers used once, generated by the access point (AP) and client respectively. 

* **MAC addresses**: unique identifiers attached to hardware, these are issued by the manufacturer.

* **Pairwise Transient Key (PTK)**: the encryption key used for data transmission between the AP and client. This number is a combination of the PMK, ANonce, SNonce and MAC addresses of both devices.

* **Packet counter (aka nonce)**: this nonce is combined with the PTK on each transmission to create unique encryption for each data packet.

*PMK \+ ANonce \+ SNonce \+ AP MAC address \+ client MAC address \= PTK*

*PTK \+ packet counter \= a one-time, unique encryption key used generated per data packet*

This attack exploits a flaw in the key reinstallation process as part of the four-way handshake used to establish the WPA1 and WPA2 connections. The retransmission of the key installation request exists to handle a situation in which the fourth stage of the handshake, the message sent by the client confirming the encryption key installation request has been received, has been lost and allows for its retransmission. The flaw in the key reinstallation standard means that each time the third message of the handshake is received by the client, the nonce counter resets. The KRACK attack works by intercepting the client’s acknowledgement of stage three, leading the client to begin sending encrypted data. Having not received the fourth and final message in the handshake, the AP sends the third message containing the key installation instruction again, resetting the nonce to zero. The client then sends a second data packet with identical encryption to one sent previously, allowing the attacker to compare identically encrypted data packets and begin working out their original content, weakening the encryption of data sent after the counter reset.

**Network segmentation**

Network segmentation is a one-off measure requiring review at regular intervals to ensure the arrangement used is sufficient and effective.

At present, the organisation has no network segmentation meaning that the internal network is one large network. Any attacker who compromises the internal network is able to move freely within the network, and the organisation is reliant on securing internal platforms only through login credentials, software hosted firewalls, and antivirus. Subnetting, the act of dividing the internal network into smaller subnets, allows for greater user access restriction in line with the principle of least privilege, and damage mitigation in the event an attacker compromises the network. A basic example of subnetting is when an organisation has public facing Wi-Fi. This is typically segmented, reducing the risk that an attacker will use the public Wi-Fi to attack other parts of the internal network.

	*How does subnetting work?*  
Modern subnetting is typically done through Classless Inter-Domain Routing (CIDR). To understand this, it is first necessary to understand how Internet Protocol version 4 (IPv4) addresses work. An IPv4 address is a unique identifier label possessed by any device connected to the internet. It takes the form of four sets of numbers ranging from 0-255 separated by full-stop notation. An example of an IPv4 address is 192.168.1.1. Each of the four sets of numbers is referred to as an octet, and each octet comprises eight bits, or eight pieces of digital data. To create a subnet, a network mask is used based on the IPv4 address. This mask serves as a filter, setting a criteria based on the IP address of each device deciding which devices belong on a specific subnet, for example the finance team of an organisation and the software that only their team requires access to may be placed on its own subnet.

An example of a network mask may be 192.168.1.0/24. The /24 specifies the criteria for the mask and refers to the bits of the IP address given, in this case 24 bits covers the first three sets of numbers of the IP address given in the mask: any device with an IP beginning with 192.168.1 will be placed on the subnet, As the last octet of eight bits is not covered by the mask, any device with an IP address between 192.168.1.0 \- 192.168.1.255 will find itself on the subnet. 

