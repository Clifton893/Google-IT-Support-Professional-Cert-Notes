# Week 5: Defense in Depth

**Defense in depth** is the concept of having multiple, overlapping systems of defense to protect IT systems.


## System Hardening

### Disabling Unnecessary Components

- An **attack vector** is a method or mechanism by which an attacker or malware gains access to a network or system.
  - Some attack vectors are email attachments, network protocols/services, network interfaces, and user input.
- An **attack surface** is the sum of all the different attack vectors in a given system.
  - The combination of all possible ways an attacker could interact with our system, regardless of known vulnerabilities.
- Ergo, keep attack surfaces as small as possible.
- The less complex something is, the less likely there will be undetected flaws.
- Telnet access for a managed switch has no business being enabled in a real-world environment.


### Host-Based Firewall

- **Host-based firewalls** protect individual hosts from being compromised when they're used in untrusted, potentially malicious environments.
- A host-based firewall plays a big part in reducing what's accessible to an outside attacker.
- **Bastion hosts/networks** are specifically hardened and minimized to reduce what's permitted to run on them.
  - They are exposed to the Internet; but they can be used like gateways or access portals into sensitive services like core authentication servers and domain controllers.
  - This would let you implement more secure authentication mechanisms and ACLs on the Bastion hosts without making it inconvenient for your entire company.

It's good practice to keep the network that VPN clients connect to separate using both subnetting and VLANs -- this gives you more flexibility to enforce security on these VPN clients. It also lets you build additional layers of defense.

Keep in mind that if the users of the system have administrator rights, then they have the ability to *change firewall rules and configurations*. If management tools allow it, you should also prevent the disabling of the host-based firewall.


### Logging and Auditing

- A **Security Information and Event Management System (SIEMS)** is like a centralized log server; it helps make sense of all the data.
- **Normalization** is the process of taking log data in different formats and converting it into a standardized format that's consistent with a defined log structure.
- A centralized log server helps secure the system from attack.

When looking at log data, pay attention to patterns and connections between traffic.

Once logs are centralized and standardized, you can write automated alerting based on *rules*.

Your log storage needs will vary based on the amount of systems being logged, the amount of detailed logs, and the rate at which logs are created.

Examples of logging servers and SIEMS solutions include rsyslog (open source), Splunk Enterprise Security, IBM Security Qradar, and RSA Security Analytics.


### Antimalware Protection

Lots of unprotected systems would be compromised *in a matter of minutes* if directly connected to the Internet without any safeguards or protections in place.

#### Antivirus
**Antivirus software** is signature-based; it has a database of signatures that identify known malware like the unique file hash of a malicious binary, or the file associated with an infection.

Antivirus software will monitor and analyze things, like new files being created or being modified on the system, in order to watch for any behavior that matches a known malware signature.

There are two problems with antivirus software:
1. They depend on signatures distributed by the antivirus software vendor;
2. They depend on the antivirus vendor discovering new malware and writing new signatures for newly-discovered threats.

- Why are antivirus programs still recommended as a core piece of security design?
  - *It protects against the most common attacks out there on the Internet.*
- An antivirus removes the background noise of the everyday Internet attacks; and lets you focus on the more important targeted or specific threats.

- Antivirus operates on a blacklist model.
- **Binary whitelisting software** operates off a whitelist model.
  - It uses a list of known good and trusted software, and only things on the list are permitted to run.
  - It will trust software using several mechanisms:
    - A unique cryptographic hash of binaries
    - A software-signing certificate


### Disk Encryption

**Full-disk encryption (FDE)** works by automatically converting data on a hard drive into a form that cannot be understood by anyone who doesn't have the key to "undo" the conversation.

- Without knowing the encryption password/key, the data on the hard drive is just meaningless gibberish.
- File encryption secures the data; but full-disk encryption secures the operating system, system files (PW Swap, etc), and the data.
- All FDE setups have an unencrypted partition on the disk, which holds critical boot files like the kernel and bootloader.
  - These files are vulnerable to an attacker with physical access, even in an FDE device.

**Secure Boot Protocol** is part of the UEFI specification.
- It uses public key cryptography to secure encrypted elements of the boot process, by integrating code signing and verification of the boot files.
- The *platform key* configures the secure boot, and is the public key corresponding to the private key used to sign the boot files.
  - This platform key is written to firmware, and is used at boot time to verify the signature of the boot files.
  - Only files correctly signed and trusted will be allowed to execute.

FDE tools include:
- Bit Locker (Microsoft)
- FileVault 2 (Apple)
- dm-crypt (Linux)
- TrueCrypt, VeraCrypt, PGP

In FDE, the master decryption is actually used to derive a user key; this way, the credentials can be changed without actually altering the master key.

- When you implement a full disk encryption solution at scale, it's super important to think about how to handle cases where passwords are forgotten.
  - This is why many enterprise solutions have a key escrow feature.
  - **Key escrow** allows the encryption key to be securely stored for later retrieval by an authorized party.

**Home directory** or **file-based encryption** only guarantees confidentiality and integrity of files protected by encryption.


## Application Hardening

### Software Patch Management

It's critical that you make sure that you install software updates and security patches in a timely way, in order to *defend your company's systems and networks*.

The best protection is to have a good system and policy in place for your company.

Management tools make this more approachable -- like SCCM (Microsoft) or puppet (Puppet Labs), which allow admins to get an overview of what software is installed across their system fleet.

Critical infrastructure devices should be approached carefully when you apply updates -- there's always the risk that a software update will introduce a new bug that might affect the functionality of the device.


### Application Policies

Policies define boundaries; and also educate users on how to use software more securely.

A common recommendation -- or even a requirement -- is to only support or require the latest version of a piece of software.

It's generally a good idea to disallow risky classes of software by policy. Things like file sharing software and piracy-relate software tend to be closely associated with malware infections.

Understand what your users need to do their jobs.

Browser extensions and add-ons also require their own policies.

Extensions that require full access to web sites visited can be risky, since the extension developer has the power to modify pages visited.

