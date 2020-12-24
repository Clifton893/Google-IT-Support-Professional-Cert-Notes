# Week 6: Operating Systems in Practice

So far, you've learned:
- How to navigate Windows and Linux
- How to set up and manage users
- How to manage software
- How to work with disks and file systems
- How to work with processes and hardware resources

## Remote Access

### Remote Connection and SSH

[insert notes from course 1]

### Remote Connections on Windows

[insert notes from course 1]

### Remote Connection File Transfer

- **Secure copy (SCP)** is a command you can use in Linux to copy files between computers on a network.
  - It uses SSH to transfer the data
- To do this, run the `scp` command with a few flags:
  - `scp /home/user/file.txt user@IPADDRESS`

### Remote Connection File Transfer on Windows

- PuTTY supports the SCP protocol, and enables Windows computers to share files and data over a network.
- PuTTY comes with a tool called the **PuTTY Secure Copy Client**, or `pscp.exe`; it can be used to copy files similar to how the Linux SCP command works.
- Windows also uses shared to transfer files to multiple machines
  - Shared folders allow you to let other people access folders and files
  - Right-click on a folder you want to share; go over the "Share with" option; and from there, add users or groups to share the folder with.
  - To access it from other computers, open up "This PC"; go into the "Computer" tab; and you can map the folder directly to your computer with the "Map Network Drive" option
- You can share files via the `net share` command
  - It allows you do to the same thing as the GUI sharing-workflow, and you'll need to specify what kind of permissions to give users.

## Virtualization

### Virtual Machines

A **virtual instance** is a single virtual machine.


## Logging

### System Monitoring

- Recall that a log is like a computer's diary -- it records events that happen on your system.
- Logs tell us important things like errors that occurred, changes that were made, etc, and are a reliable source of information.
- The act of creating log events is called **logging**.

### The Windows Event Viewer

- In Windows, events logged by the operating system are stored in an application called the *Event Viewer*.
- You can launch the Event Viewer from the Start Menu, or by typing in `eventvwr.msc` from the run box.
- Custom Views allow you to create filters that look across all event logs, and tease out just the information you're interested in.


### Linux Logs

- Logs in Linux are stored in the `/var/log` directory
  - Recall that `/var` stands for "variable," meaning files that constantly change are kept in this directory -- and logs are constantly changing.
- `/var/log/auth.log` logs authorization and security-related events
- `/var/log/kern.log` logs kernal messages
- `/var/log/dmesg` logs system startup messages
- The one log file that logs pretty much everything on your system is the `/var/log/syslog` file
  - The only thing it doesn't log by default are off events
  - When troubleshooting issues with user machines, this directory will usually contain the most comprehensive information about your system, and should be your first stop
- Log systems do a generally good job of cleaning out log files to make room for new ones
  - This is accomplished through what's called log rotation
  - In Linux, the utility to rotate logs is called `logrotate`

#### Reading a log file

- The first field is the time stamp
  - Time stamps can appear in [Unix/epoch time]()
- The next field is the host name of the machine the event occurred on
- Next is the service that the log event is referring to
- Finally, the event that occurred


### Working with Logs

- To look at the logs in real time, you can use the `tail` command
  - Ex: `tail -f /var/log/syslog` (`-f` option for "file")


## Operating System Deployment

### Imaging Software

- Recall that to **image** a machine, is to format a machine with an image of another machine.
- This includes everything, from the operating system to the settings.
- In the IT world, installing an operating system for a fleet of computers can be made easier through tools designed to image computers.

### Operating Systems Deployment Methods

One tool we can use to image computers is a *disk cloning tool*.
- It makes a copy of an entire disk, and allows you to back up a current machine or set up a new one
- The benefit of disk cloning over a standalone installation media is that you can also install settings and folders that you might need.

An option in disk-to-disk cloning is where you connect an external hard drive to the machine you want to clone. You can connect a hard drive like your HDD or SSD into something known as an *external hard drive dock*. Then you can use any disk cloning tool of your choice.

In Linux, `dd` is a command to copy files, that's also able to clone a drive (since everything in Linux is a file).


### Mobile Device Resetting and Imaging

Mobile devices are installed with an operating system at the factory; so a **factory reset** reverts the device back to the state it was in when the device was shipped from the factory.

- Doing a factory reset while expansion storage is attached might erase data that you want to keep;
- Likewise, factory reset for many devices may leave the contents of expansion storage intact
  - You don't want to re-purpose or decommission a device with personal or proprietary information still attached.

Over time, mobile device manufacturers will release updates to the device operating system. These updates will usually be delivered *over the air*, or OTA. An OTA update is one that's downloaded and installed by the mobile device itself.

There are times when you might need to use a computer to install operating system updates. Here, you would download the update to a computer; attach the mobile device to the computer via a USB cable; and run some software on the computer that will *re-flash* the mobile device.
