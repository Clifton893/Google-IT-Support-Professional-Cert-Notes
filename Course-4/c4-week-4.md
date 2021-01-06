# Week 4: Directory Services

## Introduction to Directory Services

### What is a directory server?

A **directory server** contains a lookup service that provides mapping between network resources and their network addresses.

It's used to organize and look up organizational objects and entities, ranging from user accounts, user groups, telephone numbers, and network shares.

The ideal enterprise-quality directory server should support replication. **Replication** means that the stored directory data can be copied and distributed across a number of physically distributed servers, but still appear as one unified datastore for the querying and administering.

Replication is important because it provides redundancy, by having multiple servers available simultaneously. This means there will be minimal disruption to the service, in the event a server has a mishap.


## Centralized Management

### What is centralized management?

**Centralized management** is a central service that provides instructions to all of the different parts of an IT infrastructure.

Directory services provide centralized *authentication*, *authorization*, and *accounting*; also known as AAA.

**Role-based Access Control (RBAC)** is an easier way to manage access privileges at the group/classification level (not the individual level).

**Configuration management:** By centralizing the configuration management of your computers and software, you can create rules about how things should work in your organization.

Dedicated configuration management frameworks include *Chef*, *Puppet*, and *SCCM*.


## LDAP

### What is LDAP?

**Lightweight Directory Access Protocol (LDAP)** is used to access information in directory services over a network.

Two of the most popular directory services that use LDAP are **Active Directory** and **openLDAP**.

#### LDAP notation
- An LDAP *entry* is just a collection of information that's used to describe something.
- The format of an LDAP entry basically has a unique entry name, denoted by **dn** (or **distinguished name**)
  - Then attributes and values associated with that entry
  - **CN** is the common name of the object
  - **OU** is the organizational unit such as a group
  - **DC** is the domain component
- An example of an LDAP entry:
  - `dn: CN=name,OU=group,DC=address,DC=com


### What is LDAP Authentication?

With LDAP, there are different authentication levels that can be used to restrict access to certain directories.

In LDAP, the **Bind** operation authenticates clients to the directory server.

There are three common ways to authenticate:
- **Anonymous binding:** You aren't actually authenticating at all; depending on how it's configured, anyone could potentially access that directory.
- **Simple authentication:** You just need the directory entry name and password; this is usually sent in plain text, meaning it isn't secure at all.
- **Simple authentication and security layer (SASL):** This method can employ security protocols like TLS and Kerberos; SASL requires the client and directory server to authenticate using some method.
  - One of the most common methods is Kerberos, a network authentication protocol used to authenticate user identity, secure the transfer of user credentials, and more.


## Active Directory

### What is Active Directory?

**Active Directory (AD)** is the native directory service for Microsoft Windows.

- Active Directory can communicate via the LDAP protocol; and thus can interoperate with Linux, OSX, and other non-Windows hosts via the protocol.
- AD also becomes the central repository of *group policy objects (GPOs)*, which are ways to manage the configuration of Windows machines.

The **Active Directory Administrative Center (ADAC)** is a tool for performing tasks through AD.

Like with file systems, directory services are hierarchical.

- Everything you see in AD is an object.
  - Some objects are *containers*, which can contain other objects.
- Several of the default containers are just called "containers," and they serve as default locations for certain types of objects.
- Another type of container is called an *organizational unit (OU)*, which is like a folder or directory for organizing objects within a centralized management system.
- Ordinary containers can't contain other containers; but OUs can contain other OUs.

- In ADAC, a domain will have a short name (like "example"), and a DNS name (like "example.com")
- Objects -- particularly computers in the domain -- will be given a DNS name that lives in the domain's DNS zone.
  - A **forest** is the hierarchical level above a domain; a forest contains one or more domains.
  - AD accounts can share resources between domains in the same forest.
- Computer accounts are created when a computer is joined to the AD domain.

The service that hosts copies of the AD database are called **domain controllers (DCs)**. DCs provide several services on the network:
- Domain controllers get to decide when computers and users can log onto the domain.
  - They host a replica of the AD database and group policy objects;
  - They serve as DNS servers
  - They provide central authentication via Kerberos
  - They get to decide who has access to shared resources like filesystems and printers.

It's common for most domain controllers in the AD network to be the **read-write replicas**. This means that each have a complete copy of the AD database and can make changes to it; and these changes are then replicated to all other copies of the database on other DCs. 

Some changes to the AD database can only be made safely by one DC at a time; these changes are tasked to a single DC by granting it a **Flexible Single-Master Operations (FSMO)** role.

Joining a computer to Active Directory means two things:
1. AD knows about the computer and has provisioned a **computer account** for it;
2. The computer knows about the Active Directory domain and authenticates with it.


### Managing Active Directory

- When an Active Directory domain is first set up, it contains a default user account, administrator, and several default user groups.
- Here are some of the most important user groups:
  - **Domain admins** are the administrators of the AD domain. They are like root administrators, and possess incredible privileges and powers. You should never use this as your day-to-day account, instead opting for a domain controller account.
  - **Enterprise admins** are administrators, and have permissions to make changes that affect other domains in multi-domain forests. These should only be needed on rare occasions, like when an AD forest is being upgraded to a new version.
  - **Domain users** contain every user account in the domain.
  - **Domain computers** contains all computers joined to the domain, except domain controllers.
  - **Domain controllers** contains all domain controllers in the domain.
- If there are some administrative tasks that you need to perform a lot as a part of your day to day job but you don't need to have broad access to make changes in AD, then **delegation** is for you. 
  - Just like you can set NTFS DACLs to give accounts permission in the file system, you can set up ACLs on Active Directory objects.


### Managing Active Directory Users and Groups

The **Security Account Manager (SAM)** is a database in Windows that stores username and passwords. (This is where SamAccountName comes from.)

Everything you do in ADAC is actually done in PowerShell. 
- There's a "WINDOWS POWERSHELL HISTORY" pane, which shows the commands being run by ADAC.
- You can take an example like this and generalize it to create a script that can be used to repeat this process hundreds of thousands of times.
- To describe the full path of an object in AD, LDAP is often used.

There are two categories of group in AD:
- The most common one is called a **security group**
  - Security groups contain user accounts, computer accounts, and other security groups
  - The default groups (domain users, domain admins) are security groups
  - They're used to grant or deny access to IT resources
- The other type is a **distribution group**
  - A distribution group is only designed to group accounts and contacts for email communication
  - You can't use distribution groups for assigning permissions to resources.

Group scope has to do with the way that group definitions are replicated across domains.
- Keeping many large groups synchronized in a large network is a complicated problem;
- Active Directory uses group scopes to manage that complexity.
  - **Domain local:** This is used to assign permission to a resource.
  - **Global:** This is used to group accounts into a role.
  - **Universal:** This is used to group global roles in a forest.
    - Domain Local and Global groups aren't replicated outside of the domain they're defined in; but universal groups are.
    - Universal groups are replicated to all domains in a forest.


### Managing Active Directory User Passwords

- With certain exceptions, AD doesn't store user passwords -- it stores a one-way cryptographic hash of the password.
- If there's more than one person who can authenticate using the same username and password, then auditing becomes difficult or even impossible.
- To audit your infrastructure, in this sense, means to analyze who performed specific actions in your IT infrastructure.


### Joining an Active Directory Domain

Recall that joining a computer to Active Directory means two things:
1. AD knows about the computer and has provisioned an account for it;
2. The computer knows about the AD domain and authenticates with it.

A Windows computer that isn't joined to a domain is called a *workgroup computer*; the name comes from Windows workgroups, which are a collection of standalone computers that work together. Windows workgroups aren't centrally administrated, so they become harder and harder to manage as the network grows in size.

A computer can be in a domain or in a work group, but not at the same time.

Different versions of Active Directory are referred to as **functional levels**; an AD domain has a functional level that describes the features that it supports.


### What is a Group Policy?

**Group Policy Object (GPO)**: A set of policies and preferences that can be applied to a group of objects in the directory.
- **Policies** are settings that are reapplied every few minutes, and aren't meant to be changed even by the local administrators.
  - By default, policies are reapplied on the machine every 90 minutes.
- **Preferences** are settings that, in many cases, are meant to be a template for settings.
  - Someone using the computer can change the settings from what's defined in the policy, and that change won't be overwritten.

When you *link* a GPO, all of the computers or users under that domain, site, or OU will have that policy applied.

A GPO can contain computer configuration, user configuration, or both.

When a domain-joined computer or user signs into the domain by contacting a domain controller, that domain controller gives the computer a list of group policies it should apply.

When a domain-joined computer or user signs into the domain by contacting a domain controller, that domain controller gives the computer a list of group policies that it should apply. The computer then downloads those policies from a special folder called SYSVOL, that's exported as a network share from every domain controller. This folder's replicated between all of the domain controllers and can also contain things like log in and logoff scripts. Once the computer has downloaded its GPOs, it applies them to the computer.

Many policies and preferences in GPOs are represented as values in the Windows Registry. The **Windows Registry** is a hierarchical database of settings that Windows (and many Windows applications) use for storing configuration data.


### Group Policy Inheritance and Precedence

Precedence
RSOP


### Group Policy Troubleshooting

[ notes ]

### Mobile Device Management (MDM)

- MDM solutions will let you remote wipe a mobile device.
  - A **remote wipe** is a factory reset that you can trigger from your central MDM, rather than having to do it in person on the device.
- MDM policy settings are specific to each mobile OS; but these policies can be created and distributed using an **Enterprise Mobile Management (EMM)** system.


## OpenLDAP

### What is OpenLDAP?

OpenLDAP can be used on any operating system, including Windows, Linux, and MacOS.


### Managing OpenLDAP

- You can use the command line to manage OpenLDAP; but it's easier to setup phpLDAPadmin.
- To use command line tools, you need to use LDIF files.
