# Week 1: Understanding Security Threats

## Malicious Software

### The CIA Triad

#### CIA
- **C**onfidentiality
- **I**ntegrity
- **A**vailability

Every aspect of security revolves around these three principles.

- **Confidentiality** means keeping things hidden
- **Integrity** means keeping our data accurate and untampered with
- **Availability** means the information we have is readily accessible to those people who should have it


### Essential Security Terms

- **Risk:** The possibility of suffering a loss in the event of an attack on the system.
- **Vulnerability:** A flaw in the system that could be exploited to compromise the system.
- **0-day vulnerability (zero day):** A vulnerability that is not known to the software developer or vendor, but is known to an attacker.
- **Exploit:** Software that is used to take advantage of a security bug or vulnerability.
- **Threat:** The possibility of danger that could exploit a vulnerability.
- **Hacker:** Someone who attempts to break into or exploit a system.
  - *Black hat hackers* try to get into systems to do something malicious;
  - *White hat hackers* attempt to find weaknesses in a system to fix them before someone can do something malicious.
- **Attack:** An actual attempt at causing harm to a system.


### Malicious Software

**Malware** is a type of malicious software that can be used to obtain your sensitive information, or delete or modify files.

#### The most common malware
- Viruses
- Worms
- Adware
  - Software that displays advertisements and collects data
- Spyware
  - A type of malware that's meant to spy on you
  - A *keylogger* is a common type of spyware that's used to record every keystroke you make
- Trojans
  - Malware that disguises itself as one thing but does something else
- Rootkits
  - A collection of software or tools that an Admin would use
- Backdoors
  - A way to get into a system if the other methods to get in the system aren't allowed
  - Most commonly installed after an attacker has gained access to your system and wants to maintain access
- Botnets
  - Designed to utilize the power of the Internet-connected machines to perform some distributed function
  - Compromised machines are known as *bots*
  - A collection of one or more of these machines is called a *botnet*
- Ransomware
  - A type of attack that holds your data or system hostage until you pay some sort of ransom
- Logic bomb
  - A type of malware that's intentionally installed; after a certain event or time has triggered, it will run the program.


## Network Attacks

### Network Attacks

#### DNS Cache Poisoning attack
- Works by tricking a DNS server into accepting a fake DNS record that will point you to a compromised DNS server
- It then feeds you fake DNS addresses when you try to access legitimate websites
- DNS cache poisoning can spread to other networks, too, if the servers are getting their DNS information from a compromised server

#### Man-in-the-middle attack
- An attack that places the attacker in the middle of two hosts that think they're communicating directly with each other
- A common MitM attack is a *session hijacking* (or a *cookie hijacking*)
- Another MitM method is a **rogue access point** attack;
  - An access point that is installed on the network without the network administrator's knowledge
- A final MtM method is called an *evil twin* 
  - The premise of an evil twin attack is for you to connect to a network that is identical to yours (controlled by the attacker)


### Denial-of-Service

A **Denial-of-service (DOS) attack** is an attack that tries to prevent access to a service for legitimate users by overwhelming the network or server.

A **distributed denial-of-service attack (DDoS)** is a DoS attack using multiple systems.

The **ping of death (POD)** works by sending a malformed ping to a computer; the ping would be larger than what the IP was made to handle, so it results in a buffer overflow, causing the system to crash and potentially allow for execution of malicious code.

**Ping flood** sends a ton of ping packets to a system -- ICMP echo requests; if the computer can't keep up with the echo replies, it could be overwhelmed and taken down.

**SYN flood** (half-open attacks) the server is bombarded with SYN packets, not replying to SYN-ACK packets; thus the connection stays open and takes up the server's resources, not allowing other users to connect to the server.


## Other Attacks

### Client-Side Attacks

**Injection attacks** 
- Can be mitigated with good software development principles, like validating input and sanitizing data

**Cross-site scripting (XSS) attacks** are a type of injection attack where the attacker can insert malicious code and target the user of the service.
- XSS attacks are a common method to achieve a session hijacking.

**SQL injection attack** targets the entire website, if the website is using a SQL database.
- Attackers can potentially run SQL commands that allow them to delete website data, copy it, and run other malicious commands.


### Password Attacks

**Password attacks** use software like password-crackers that try and guess your password.

A common password attack is a **brute force attack**, which just continuously tries different combinations of characters and letters until it gets access.

Another type of password attack is a **dictionary attack**, which tries out words that are commonly used in passwords.

Good passwords are at least 8 characters, and a mix of capital, lower-case, alphanumeric, and symbolic characters.


### Deceptive Attacks

**Social engineering** is an attack method that relies heavily on interactions with humans instead of computers.

A **phishing attack** usually occurs when a malicious email is sent to a victim disguised as something legitimate.

**Spear phishing** specifically targets an individual or group.

**Spoofing** is when a source masquerades around as something else.

**Baiting** is used to entice a victim to do something through physical contact.

**Tailgating** is gaining access into a restricted area or building, by following a real employee in.

