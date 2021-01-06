# Week 2: System Administration and IT Infrastructure Services

## Intro to IT Infrastructure Services

### What are IT Infrastructure Services?

IT infrastructure services are what allow organizations to function. These include:
- Connecting to the Internet;
- Managing networks by setting up the network hardware;
- Connecting computers through an internal network;
- And many other tasks.


### Types of IT Infrastructure Services
You can buy or rent hardware for your servers and set them up on-site or somewhere else. 

#### Infrastructure as a Service

You can also use the cloud alternative to maintain your own infrastructure, which is called **Infrastructure as a Service (IaaS)**.
- IaaS providers give you preconfigured virtual machines you can use just as if you had a physical server
- Popular providers include:
  - Amazon Web Services and their Elastic Compute Cloud (EC2) instances
  - Linode
  - Windows Azure
  - Google Compute Engine

#### Networking as a Service (NaaS)

Networking can be integrated in an IaaS provider, but it's branched off in recent years into its own cloud service: **Networking as a Service (NaaS)**.
- NaaS allows companies to offshore their networking services, so they don't have to deal with expensive networking hardware
- Companies also won't have to set up their own network security, manage their own routing, set up a WAN and private Internets, etc.

#### Software as a Service (SaaS)

For software your company may require (word processors, spreadsheets, email clients, OS, etc), the cloud alternative to maintaining your own software is known as **Software as a Service (SaaS)**. These are services you can purchase that allow you to use them from a web browser.

#### Platform as a Service (PaaS)

If you want an all-in-one solution to building and deploying a web application, you can use something called **Platform as a Service (PaaS)**. 
- This includes an entire platform that allows you to build code, store information in a database, and serve your application from a single platform
- Popular options for PaaS are Heroku, Windows Azure, and Google App Engine

#### Managing Users, Access, & Authorization

A **directory service** centralizes your organization's users and computers in one location, so that you can add, update, and remove users and computers.
- Two of the most popular directory services are Windows Active Directory, and OpenLDAP
- Directory services can also be deployed in the cloud using **Directory as a Service (DaaS)**


## Physical Infrastructure Services

### Server Operating Systems

- For an organization, you'll typically want to install your services on a server operating system.
- A **server operating system** is a regularly operating system that is optimized for server functionality.
- These include functions like allowing more network connections, and more RAM capacity.
- Most operating systems have versions specifically made for servers:
  - Windows Server
  - Ubuntu Server
  - MacOS Server
- Server operating systems are usually more secure and come with additional services already built in.


### Virtualization

There are two ways you can run your servers:
1. Either on dedicated hardware;
2. Or on a virtualized instance on a server.

#### Performance
- A service running on dedicated hardware will have better performance than a service running in a virtualized environment
- This is because you only have one service using one machine, as opposed to many services using one machine.

#### Cost
- Server hardware can be expensive
- With virtualization, you can have ten services running on ten different virtual instances, all on one physical server
- It's cheaper to run several services on one machine than it is to run many services on multiple machines.

#### Maintenance
- Servers require hardware maintenance and routine operating system updates.
- Sometimes, you'll need to take the servers offline to do that maintenance.
- Virtualized service makes server maintenance much easier to do.
- With virtualized service, you can quickly stop the service, migrate it to another physical server, and take as much time as you need for maintenance.

#### Points of Failure
- Service on one physical machine can be trouble, if that machine has issues.
- You can easily move virtualized service off a machine and spin up the same service on a different machine as a backup.
- You can prevent a single point of failure on a physical machine if you have redundant servers set up (duplicate servers as a backup)


### Remote Access Revisited

- In Linux, the most popular remote access tool is OpenSSH
- To SSH into another machine:
  - You need to install an SSH client on the machine your connecting from;
    - `sudo apt-get install openssh-client`
  - And install an SSH server on the machine your'e connecting to.
    - `sudo apt-get install openssh-server`


## Network Services

### FTP, SFTP, and TFTP

File transfer services are a popular network use for organizations. A server dedicated to file transfer allows you to store huge directories and files; and transfer them from one computer to another using the Internet.

**File Transfer Protocol (FTP)** is a legacy way to transfer files from one computer to another over the Internet. It's still in use today.
- It's not the most secure way to transfer data, because it doesn't handle data encryption.
- It operates not too unlike an SSH service -- to access an FTP server, a computer has to install an FTP client
- FTP is still primarily used to share web content.

**Secure File Transfer Protocol (SFTP)** is a version of FTP that uses SSH and encrypts its files.

**Trivial File Transfer Protocol (TFTP)** is a simpler way to transfer files -- it doesn't require user authentication (which FTP does).
- A popular use of TFTP is to host installation files, booting computers through **preboot execution (PXE Boot)**


### NTP

One of the oldest Internet protocols in use today is the **network time protocol (NTP)**. It's used to keep the clock synchronized on machines connected to a network.

There are different ways to set up an NTP server:
- You can use a *local NTP server*, where you install NTP server software on your management server
  - Then, you install NTP clients on your machines, and tell those computers which NTP service to sync their time to.
- Or, you can use a *public NTP server*
  - These are managed by other organizations that your client machines connect to, in order to get synchronized time.
  - It's better etiquette to run your own NTP servers if you have a large fleet of machines.


### Network Support Services Revisited

#### Intranets
- An Intranet is an internal network inside a company
- It can house documentation, updates, and many other resources

#### Proxy Servers
- A proxy server acts as an intermediary between a company's network and the Internet.
- They receive traffic, and relay that traffic to the company network
  - This way, company network traffic is kept private from the Internet
- Proxy servers can also be used to monitor and log internal company network activity


### DNS

As a recap, **Domain Name System (DNS)** maps human-understandable names to IP addresses.

#### For Web Servers
If you own the domain name and host your web content yourself, it make sense for you to have the DNS servers that know that information.

#### For Internal Networks
- The other reason we might want our own DNS servers is so we can map our own internal computers to IP addresses
  - That way, we can reference a computer by name, instead of an IP address
- *Local host* is a common way to access a local web server.
- A DNS query first checks the local host file, then it checks the local DNS servers
  - But manually configured every single computer's local host files is not efficient
- Instead, you can set up a local DNS server that contains all the names mapped to their IP addresses
  - Then, you change the local network settings for all computers to use the DNS sever instead of the one given by the local ISP.
- Another option is to integrate your internal network with a directory service which handles user and machine info in its central location, like Active Directory
  - Once you set up DNS in your directory service, it will automatically populate with machine-to-IP address mappings (not manually)


### DHCP

- Recall that through DHCP, your computers will be "leased" an IP address from a DHCP server.
  - They automatically get IP addresses, you needn't manually set anything, and it makes expanding your IP address range an easy task (handled automatically)
- If you want to integrate DHCP with DNS, you need the address of your local DNS servers, what gateway you should assign, and the subnet mask that gets used.
- Then you have to configure the DHCP server software with this new information.
- By syncing the DNS and DHCP servers, whenever DHCP leases out new addresses, DNS updates IP address mappings automatically.



## Troubleshooting Network Services

### Unable to Resolve a Hostname or Domain Name

There are some situations where DNS can be tricky to navigate, since there can be many contributing factors. But as with any troubleshooting scenario, remember to keep isolating the problem down until you can get to a root cause.


## Managing System Services

### What Do Services Look Like in Action?

- Services such as DNS, DHCP, NTP, and others are **background processes**
  - Also known as **daemons** or **services**.
- This means the program doesn't need to interact with the user through the GUI or CLI to provide the necessary service.
  - The operating system ensures that the program is running.
- Each service has one or more **configuration files**, that you as a sysadmin will use to determine how you want the service to behave.
  - Services are usually configured to start when the machine boots, so that if there's a power outage or a similar event that causes the machine to reboot, you won't need a system administrator to manually start the service.


### Managing Services in Linux

You can check if there's an NTP daemon running on a Linux machine using the service command `service ntp status`

### Managing Services in Windows

In Windows PowerShell, `Stop-Service`, `Start-Service`, and `Get-Service` can be used to manage daemons.

You can list all services that are registered in the system using the `Get-Service` command; or through using the GUI's Services management console.


### Configuring Services in Linux

- Most services are enabled as soon as you install them. These are programs that are shipped with the defaults, that are good enough to safely start serving right away
- But not all services can provide default values that are suitable -- you will need to edit the configuration files before the service can go live.
- In Linux, the configuration files for the installed services are located in the `/etc` directory.

**lftp** is an FTP client program that allows us to connect to an FTP server.

**Reload** means the service re-reads the configuration without having to stop and start. This way, ongoing connections aren't interrupted, but new connections will use a new configutation.


### Configuring Services in Windows

As an example, you can access Windows's Internet Information Services (the feature offered by Windows to serve web pages) through Start > Control Panel > Turn Windows features on and off

You can configure through the GUI from here. (In this example, to install a web server services feature.)
