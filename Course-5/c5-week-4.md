# Week 4: Securing Your Networks

## Secure Network Architecture

### Network Hardening Best Practices

**Network hardening** is the process of securing a network by reducing its potential vulnerabilities through configuration changes and taking specific steps.

**Implicit deny** is a network security concept where anything not explicitly permitted or allowed should be denied.



**Analyzing logs** is the practice of collecting logs from different network (and sometimes, client) devices on your network, then performing an automated analysis on them.

You'd want to analyze things like firewall logs, authentication server logs, and application logs.

- **Logs analysis systems** are configured using user-defined rules to match interesting or atypical log entries.
- **Normalizing log data** is an important step, since logs from different devices and systems may not be formatted in a common way.
- You might need to convert log components into a common format to make analysis easier for analysts, and rule-based detection systems, this also makes correlation analysis easier.
- **Correlation analysis** is the process of taking log data from different systems and matching events and matching events across the systems.
- A **post-fail analysis** investigates how a compromise happened after the breach is detected.

**Splunk** is a popular and powerful logs analysis system, offering flexible and extensible log aggregation and search system. It can grab logs data from a wide variety of systems, and in large amounts of formats. It can also be configured to generate alerts, and allows for powerful visualization of activity based on logged data.

**Flood guards** provide protection against DoS or Denial of Service attacks.

*fail2ban* is a popular open source flood guard tool.

**Network separation** or **network segmentation** is a good infosec principle, permitting more flexible management of the network and providing security benefits.  This is the concept of using VLANs to create virtual networks for different device classes/types. It's like creating dedicated virtual networks for your employees to use, and also having separate networks for your printers to connect to. The idea is that printers won't need access to the same network resources that employees do.


### Network Hardware Hardening

Recall that **DHCP** is the protocol where devices on a network are assigned critical configuration information for communicating on the network.

A **rogue DHCP server attack** is when an attacker deploys a server on your network, able to hand out DHCP leases with whatever information they want -- including setting a gateway address or DHCP server that's actually a machine within their control. This gives them access to your traffic and opens the door for future attacks.

#### DHCP snooping
- **DHCP snooping** is an enterprise switch-level feature that protects against rogue DHCP server attacks.
  - It monitors DHCP traffic being sent across it
  - It also tracks IP assignments and maps them to hosts connected to switch ports, building a map of assigned IP addresses to physical switch ports.
  - This info can also protect against IP spoofing and RP poisoning attacks.
- DHCP snooping makes you designate either a trusted DHCP server IP, or enable DHCP snooping trust on the uplinked port.
  - Thus any DHCOP responses coming from either an untrusted IP address or from a downlinked switch port would be detected as untrusted, and discarded by the switch.


#### Dynamic ARP inspection
- Recall that ARP allows for man-in-the-middle attacks because of the unauthenticated nature of ARP, allowing attackers to forge an RP response, advertising its MAC address as the physical address matching a victim's IP address.
  - This is called a *gratuitous ARP response*.
- **Dynamic ARP inspection (DAI)** is another enterprise switch-level feature that prevents this attack.
  - It requires use of DHCP snooping to establish a trusted binding of IP addresses to switch ports.
  - DAI will detect forged gratuitous ARP packets and drop them;
  - It does this because it has a table from DHCP snooping that has the authoritative IP address assignments per port.
  - DAI also enforces rate limiting of ARP packets per port, to prevent ARP scanning.

#### IP Source Guard
- To prevent IP spoofing attacks, **IP Source Guard (IPSG)** can be enabled on enterprise switches along with DHCP snooping.
- IPSG works by using the DHCP snooping table to dynamically create ACLs for each switchboard.
  - It drops packets that don't match the IP address for the port based on the DHCP snooping table.

#### 802.1X
- This is the IEEE standard for encapsulating **Extensible Authentication Protocol (EAP)** traffic over the 802 networks.
- This is also called **EAP over LAN**, or **EAPOL**.
- It was originally designed for Ethernet; but support was added for other network types like WiFi and fiber networks.
- **EAP-TLS** is one of the more common and secure EAP methods.

##### EAP-TLS
- When a client wants to authenticate to a network using 802.1X, there are 3 parties involved:
  1. The client device (what we call the *supplicant*)
    - Also refers to software running on the client machine that handles authentication, like the open source Linux utility `wpa_supplicant`
  2. The authenticator
  3. The authentication server

- The supplicant communicates with the authenticator, which is a gatekeeper for the network.
  - Usually an enterprise switch or access point, requiring clients to successfully authenticate to the network before they're allowed to communicate with the network.
  - The authenticator doesn't actually authenticate -- it sends the request to the authentication server.
- The authentication server -- usually a RADIUS server -- is where the actual credential verification and authentication occurs.
- **EAP-TLS** is an authentication type supported by EAP that uses TLS to provide mutual authentication of both the client and the authenticating server.
  - It's considered one of the more secure configurations for wireless security.
  - Most EAP-TLS implementations require client-side certificates.
  - Authentication can be certificate-based; or a client can use a certificate in conjunction with a username, password, or even a second factor of authentication (like a OTP).
- A more secure configuration for EAP-TLS would be to bind the client-side certificates to the client platforms using TPMs.
  - This would prevent theft of the certificates from client machines.
  - Combined with FDE, even theft of a computer would prevent compromise of the network.


### Network Software Hardening

- Network software hardening includes things like firewalls, proxies, and VPNs
  - A host-based firewall can protect other hosts from being compromised by corrupt devices on the internal network -- this is something a network-based firewall may not be able to help defend against.
- VPNs are good for providing secure access to internal resources for mobile or roaming users.
  - Recall that VPNs are commonly used to provide **secure remote access**, and **link two networks** securely.
- Proxies provide secure remote access without using a VPN; and are useful to protect client devices and their traffic.
  - A proxy server can allow web traffic to be proxied through a server that we control for many purposes.
- A reverse proxy can be configured to allow secure remote access to web-based services without requiring a VPN.


## Wireless Security

### WEP Encryption and Why You Shouldn't Use It

- Never send plaintext and ciphertext together.


### Let's Get Rid of WEP! WPA/WPA2

- Recall that **WiFi Protected Access (WPA)** was designed as a short-term replacement that would be compatible with older WEP-enabled hardware with a simple firmware update.
- **Temporal Key Integrity Protocol (TKIP)** was a new security protocol introduced to address shortcomings of WEP security. It offered 3 new feaures:
  1. More secure key derivation method
  2. Sequence counter was implemented
  3. A 64-bit message integrity check
- Under WPA, the **pre-shared key** is the WiFi password you share with people when they come over and want to use your wireless network.
  - This is not directly used to encrypt traffic -- it's a factor to derive the encryption key.
  - The passphrase is fed into the **Password-Based Key Derivation Function 2 (PBKDF2)** along with the WiFi network's SSID as a salt.

WPA2 improved WPA security by implementing **Counter Mode CBC-MAC Protocol (CCMP)**
- WPA2 is the best wireless network security available
- Pre-shared key requirements are the same

#### The Four-Way Handshake

The process that authenticates clients to the network.

1. The AP sends a nonce to the client
2. The client sends a nonce to the AP
3. The AP sends the GTK
4. The client responds with an ACK

- **Pairwise Transient Key (PTK)** is generated by:
  - PMK
  - AP nonce
  - Client nonce
  - AP MAC address
  - Client MAC address

- **Groupwise Transient Key (GTK)**
  - Updated and shared between all clients

- WPA/WPA2 also introduce an 802.1X authentication, usually called WPA2-Enterprise.
- Non-802.1X configurations are called either WPA2-Personal, or WPA2-PSK (since they use a pre-shared key to authenticate clients).

- **WiFi Protected Setup (WPS)**
  - Supports PIN entry authentication
  - NFC or USB
  - Push-button authentication
- The PIN authentication mode where the AP has a PIN hard-coded into the firmware is vulnerable to an online brut force attack.
- The PIN is 8 digits long; but the 8th digit is a checksum computed from the first 7 digits.


### Wireless Hardening

In an ideal world, we'd all be protecting our wireless networks with **802.1X with EAP-TLS**.

If 802.1X is too complicated for a company, the next best alternative would be **WPA2 with AES/CCMP mode**.

A long and complex passphrase that wouldn't be found in a dictionary would increase the amount of time and resources an attacker would need to break the passphrase.

If your company values security over convenience, you should make sure that WPS isn't enabled on your APs.


## Network Monitoring

### Sniffing the Network

- **Packet sniffing (packet capture)** is the process of intercepting network packets in their entirety for analysis.
- **Promiscuous Mode** is a type of computer networking operational mode in which all network data packets can be accessed and viewed by all network adapters operating in this mode.
  - If the packets aren't going to be sent to your interface in the first place, Promiscuous Mode won't help you see them.
- **Port mirroring** allows the switch to take all packets from a specified port, port range, or entire VLAN and mirror the packets to a specified switch port.
- **Monitor mode** allows us to scan across channels to see all wireless traffic being sent by APs and clients.

If a wireless network is encrypted, you can still capture the packets; but you won't be able to decode the traffic payloads without knowing the password for the wireless network.


### Wireshark and tcpdump

**tcpdump** is a super popular, lightweight, command-line based utility that you can use to capture and analyze packets.

**Wireshark** is also a packet capture and analysis tool, way more powerful when it comes to application and packet analysis (compared to tcpdump).

Traffic analysis is an important part of network security -- being able to capture and inspect those packets is important to understanding what type of traffic is flowing on our networks that we'd like to protect.


### Intrusion Detection / Prevention System

- **Intrusion Detection and Prevention Systems (IDS/IPS)** operate by monitoring network traffic and analyzing it.
- These look for matching behavior or characteristics that would indicate malicious traffic.
- IDS is only a detection system -- it won't take action to block or prevent an attack when one is detected.
  - It will only log an alert.
- But an IPS system can adjust firewall rules on the fly, to block or drop the malicious traffic when it's detected.
- IDS/IPS can be either host-based or network-based.

- A **Network Intrusion Detection System (NIDS)** detection system would be deployed somewhere on a network where it can *monitor traffic* for a network segment or subnet.
- NIDS are similar to firewalls
  - But firewalls prevent intrusion by potentially malicious traffic coming from outside the network (enforcing ACLs in between);
  - Whereas NIDS systems are meant to detect and alert potential malicious activity coming from within the network.
- A NIDS device is a passive observer, unlike a NIPS.

- **Port mirroring functionality** (found in many enterprise switches) is a good way to get access to network traffic.
  - It allows all packets on a port, port range, or entire VLAN to be mirrored to another port -- where a NIDS host would be connected.

A NIDS host must have at least two network interfaces:
1. For monitoring and analysis;
2. One for connecting to our network, for management and administrative purposes.

Placement of a **Network Intrusion Prevention System (NIP)S** would differ from a NIDS system.
- A NIPS must be placed in-line with the traffic being monitored -- meaning the traffic must pass through the NIPS device.


