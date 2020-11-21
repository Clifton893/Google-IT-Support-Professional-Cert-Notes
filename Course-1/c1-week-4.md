# Week 4: Networking

<!-- insert Table of Contents here -->

## What is Networking?

### Basics of Networking

*"The Internet is just an interconnection of computers around the world, like a giant spider web that brings all of us together."*

- We call the interconnection of computers a **network**.

The Internet is *not* the World Wide Web.

- **The Internet** is the physical connection of computers and wires around the world.

- **The Web** is the information on the Internet.

**Networking** in the IT field is managing, building, and designing networks.

- You don't connect to the Internet directly; instead, computers called *servers* connect directly to the Internet.
  - These machines serve content like websites, hence the name.
  - **Clients** request the content from servers. 
  - Clients don't connect directly to the Internet; they connect to an **internet server provider (ISP)**.

- Computers on a network have an identifier called an **IP address**.

- Devices that can connect to a network have another unique identifier called a MAC address.
  - ***Media access control (MAC) addresses** are generally permanent and hard-coded onto a device.*

- When you send or receive data through a network, you need to have both an *IP* and a **MAC** address.

- An analogy is the addresses on a letter:
  - The IP address is your home address;
  - The MAC address is the name of the recipient (making sure it gets to the right location and right person)

- Data sent through a network is sent through a network is sent through **packets**
  - Little bits of data, in 1s and 0s.
  - When a packet gets to its destination, it will rearrange itself back in order.


### Networking Hardware

- **Ethernet cable** lets you physically connect to the network through a cable.

- **Wi-Fi** is wireless networking.

- **Fiber-optic cables** allow greater speeds than all other methods. Named for its glass fibers that transfer 1s and 0s through light, not electrical current.

Computers connect to a few different devices that help organize our network together:
- **Router:** Connects lots of different devices together and helps route network traffic (through *network protocols*).
- **Switches** are like mailrooms in a building.
  - Routers get our letters to the building; 
  - But once we're inside, we use the mailroom to figure out where to send a letter.
- **Hubs** are like company memos.
  - They don't know who to send the memo to, so they send it to everyone.

- **Network stack:** A set of hardware or software that provides the infrastructure for a computer.
  - It is all the components that makes up computer networking.

*"You might need to investigate the networks stack and your job. You'd start with making sure the end user computers are working properly. Then you'd turn your attention to other possible points of failure like the cabling, switches and routers, that work together to access the Internet."*


### Language of the Internet

- Network protocols have rules that ensure your data packets:
  - Are routed efficiently;
  - Aren't corrupted;
  - Are secure;
  - Go to the right machine;
  - Are named appropriately.

**TCP/IP** have become the predominant protocols of the Internet.

- The **Internet Protocol (IP)** is responsible for delivering packets to the right computers.
  - The IP helps us route information, through the use of IP addresses.

- The **Transmission Control Protocol (TCP)** is responsible for delivering information from one network to another. 


### The Web

- **Websites** are basically text documents formatted with *HTML*.

- **Hypertext Markup Language (HTML)** is a coding language used by web browsers.

- **Uniform Resource Locator (URL)** is a web address, similar to a home address.

- The part after `www.` in a web address is called the **domain name**.
  - Once a domain name is registered with the Internet Corporation for Assigned Names and Numbers (ICANN), no one else can take that name unless it becomes available again.

- **Domain name system (DNS)** acts like the Internet's directory, using human-readable words to map to an IP address.
  -*"Every time you go on a website, your computer is performing a DNS lookup to find the IP address of the website name you typed in."*

- The source of Internet requests are usually identified by IP addresses and server logs. 


## Limitations of the Internet

### History of the Internet

- The United States initiated the DARPA project in the 1960s
  - This would create the ARPANET, the earliest version of the Internet
  - Programmers could now remotely access a computer; but networks still couldn't talk to each other.
- In the 1970s, computer scientists Vinton Cerf and Bob Kahn created the TCP/IP.
  - *The TCP/IP protocol is what allowed computers to share information outside their network, which stemmed the creation of the Internet as we know it today.*
  - Over the next 50 years, TCP/IP would grow as the standard, and it remains so today.
  - But the data sent was just text, and not centralized.
- The 1990s, Tim Berners-Lee creates the World Wide Web, which used different protocols for displaying information in webpages.

### Limitations of the Internet

- Finite IP addresses

- The current protocol of IP, **Internet Protocol version 4 (IPv4)** is an address that made up of 32 bits separated into 4 groups (four bytes).
  - Remember that 1 byte can store up to 256 values (0 - 255).
  - Thus, an example of an IPv4 address would be `73.55.242.3`
- This is limited, since there are less than 4.3 billion IPv4 addresses, and *over* 4.3 billion websites on the web today.

- IPv6 addresses consist of 128 bits -- four times more than IPv4.
  - Adoption of IPv6 is slow, but steady.

- **Network Address Translation (NAT)** lets organizations use one public IP address and many private IP addresses within the network.
  - Think of it like a business's receptionist, who transfers calls to private numbers inside the business.


## Impact of the Internet

### Impact

- **Globalization** is the movement that lets governments, businesses, and organizations communicate and integrate together on an international scale.

### Internet of Things

- The **Internet of Things** refers to the integration and interconnection of smart devices.

- Further reading: [What is the Internet of Things? WIRED explains](https://www.wired.co.uk/article/internet-of-things-what-is-explained-iot)

### Privacy and Security

- Privacy is no longer a personal issue, it's a matter of national security.

- **Children's Online Privacy Protection Act (COPPA)** regulates the information you show to children under the age of 13.

- Copyright and intellectual property theft is also a massive subject of online policy.

- Computer security is no longer the job of specialist engineers--it's the job of *everybody*.

*Prepare for being hacked, by understanding how hacking works.*

---

## Questions for review

### Keywords
<details>
  <summary>What is a network?</summary>
  <p>An interconnection of computers.</p>
</details>

<details>
  <summary>What is the Internet?</summary>
  <p>The physical connection of computers and wires around the world.</p>
</details>

<details>
  <summary>What is an IP address?</summary>
  <p>An Internet protocol (IP) address is an identifier for computers on a network.</p>
</details>

<details>
  <summary>What is a MAC address?</summary>
  <p>Media access control (MAC) addresses are unique identifiers for hardware, generally permanent and hard-coded onto a device.</p>
</details>

<details>
  <summary>What is the DNS?</summary>
  <p>The domain name system (DNS) acts like the Internet's directory, and uses human-readable words to map an IP address.</p>
</details>

<details>
  <summary>What is NAT?</summary>
  <p>Network address translation (NAT) lets organizations use one public IP address, and many private IP addresses, within a network.</p>
</details>

<details>
  <summary>What is the Internet of Things?</summary>
  <p>The Internet of Things refers to the integration and interconnection of smart devices.</p>
</details>

### Concepts

<details>
  <summary>What is the process of connecting to the Internet?</summary>
  <p></p>
</details>

<details>
  <summary>What is the difference between the TCP and IP?</summary>
  <p></p>
</details>

<details>
  <summary>Why was the creation of TCP/IP so important in networking history?</summary>
  <p></p>
</details>
