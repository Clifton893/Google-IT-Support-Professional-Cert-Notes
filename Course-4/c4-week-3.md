# Week 3: Software and Platform Services

## Software Services

**Software services** are the services that employees use that allow them to do their daily job functions.

**Platform services** provide a platform for developers to code, build, and manage software applications.


### Configuring Communication Services

There are several methods of instant communication, in the business environment.

**Internet Relay Chat (IRC)** is a protocol that's used for chat messages. IRC operates in a client & server model, so lots of IRC client software can be used to connect to an IRC server.

Open IM Protocols

**Extensible Messaging and Presence Protocol (XMPP)** is an open-source protocol used in instant messaging applications and social networking services. Pidgin and Padium are two free applications that use XMPP.


### Configuring Email Services

To configure email services for the company, you need to have a domain name set up that you can use as the email domain (such as employee@ccompany.com).

There are two ways to set up email for a company
1. Run your own managed server
  - You set up the email service software on a server, then you create a DNS record for your mail server.
  - Remember that the **A record** is used for hostnames; but for email servers, we use **MX** for the **mail exchange record**.
2. Use an email service provider (like Google Suite)

#### Email protocols

**Post Office Protocol version 3 (POP3)** is an email protocol that downloads email from an email server onto your local device. It deletes the email from the email server, meaning you can only view the email from one device.
- Good for keeping your email storage under a certain quota
- Since your email can only be seen from your local device, POP3 has privacy benefits as well

**Internet Message Access Protocol (IMAP)** allows you to download emails from your email server onto multiple devices, and keeps your messages on the email server.
- This is one of the most popular ways to retrieve email

**Simple Mail Transfer Protocol (SMTP)** is a protocol used for sending email.
- Really the only email protocol for sending email, and that's SMTP.


### Configuring User Productivity Services

When considering software licenses, it's important to review the terms and agreements.


### Configuring Security Services

**Hyper Text Transfer Protocol Secure (HTTPS)** is the secure version of HTTP, which makes sure the communication your web browser has with the website is secured through encryption.

HTTPS is also referred to as "HTTP over TLS," or "HTTP over SSL." This is because there are two protocols that enable us to make our web servers secure.

The **Transport Layer Security (TLS)** protocol is the most popular way to keep communications secure over a network. TLS is widely used to keep web browsing secure; but it can be used in many other applications, too.

The second is **Secure Socket Layer (SSL)** protocol. SSL is a way of securing communication between a web server and a client. But, it's old and insecure, and has been deprecated in favor of TLS.
- TLS and SSL are often used interchangeably
- SSL version 3.0 was essentially TLS version 1.0
- But TLS is more secure and now superior

To enable TLS on a server so the site can use HTTPS, you need a digital certificate of trust from an entity called a *certificate authority*.
- The authority grants a certificate to your website saying it trusts that you control the web server
- It also verifies that you are who you say you are


## File Services

**File storage services** allow us to centrally store files and manage access between files and groups.

### Network File Storage

**Network File System (NFS)** is a protocol that enables files to be shared over a network.

NFS works with all operating systems; but there are issues with Windows. Samba is a better alternative for a Windows fleet (and is also compatible with other operating systems)

- SMB is the protocol that Samba implements, and is *not* the same as Samba
- When you create a Windows shared folder, it's created using the SMB protocol
- Samba itself is a software service suite used for file services

Other file storage service solutions include 

#### NAS
- **Network attached storage (NAS)** are computers that are optimized for file storage
- They usually come with an operating system that's been stripped down in order to just serve files over a network; and they come with a ton of storage space.


### Mobile Synchronization

When you synchronize data, you make sure that the data is the same in two or more places.


## Print Services

### Configuring Print Services

Along with managing print essentially, you'll also need to be able to deploy printer driver software so your users can print from their computers.

To set up a print server, all you have to do is install a print service on a server.

In Linux, a common print server that's usually pre-installed on machines is the **Common UNIX Printing System (CUPS)**

A cloud service provider is another way to manage printers.


## Platform Services

### Web Servers Revisited

A **web server** stores and *serves* content to clients through the Internet.

Among the many popular types of HTTP server software, the most widely used is the **Apache HTTP server** (or just **Apache**).

### What is a database server?

**Databases** allow us to store, query, filter, and manage large amounts of data.


## Troubleshooting Platform Services

### Is the website down?

**HTTP** status codes are codes or numbers that indicate some sort of error or info messages that occurred when trying to access a web resource.

- HTTP status codes that start with `4xx` indicate an issue on the *client-side*.
- The other common HTTP status codes you might see start with `5xx`
  - These errors indicate an issue on the *server-side*.
- HTTP status codes tell us more than just errors
  - Codes beginning with `2xx` tell us when our request is *successful*.


## Managing Cloud Resources

### Cloud Concepts

When you use **Software as a Service (SaaS)**, the software is already pre-configured and the user isn't deeply involved in the cloud configuration.

When you use **Infrastructure as a Service (IaaS)**, you're hosting your own services in the cloud. You need to decide how you want the infrastructure to look, depending on what you want to run on it. (Start small; then select more powerful instances as needed.)

When you set up cloud resources, you need to consider regions. A **region** is a geographical location containing a number of data centers.
- Each of these data centers is called a *zone*, and each zone is independent of the others.
- If one of them fails for some reason, the others are still available and services can be migrated without visibly affecting users.

You might also hear about different types of clouds:
- **Public cloud:** Cloud services provided to you by a third party
- **Private cloud:** When your company owns the services and the rest of your infrastructure -- whether on-site or in a remote data center
- **Hybrid cloud:** A mixture of both public and private clouds


### Typical Cloud Infrastructure Setups

- A **load balancer** ensures that each VM receives a balanced number of queries.
- **Autoscaling** allows the service to increase or reduce capacity as needed, while the service owner only pays for the cost of the machines that are in use at any given time.
- If you need data persistence, you have to create separate storage resources to hold that data and connect that storage to the VMs.
- Most cloud providers include *monitoring* and *alerting* solutions as part of their services.


### When and How to Choose Cloud

Most cloud providers offer free trials, so it's a good idea to test that out to see if they meet your needs, and to check how well your company's infrastructure integrates with the cloud provider's.
