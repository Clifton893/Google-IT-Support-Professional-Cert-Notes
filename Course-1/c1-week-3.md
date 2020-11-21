# Week 3: Operating Systems

<!-- insert Table of Contents here -->

## What's an operating system?

### Remote Connection and SSH

- **Remote connection** allows us to manage multiple machines from anywhere in the world.

- **Secure shell (SSH)** is a protocol implemented by other programs to securely access one computer from another.
  - To use SSH, you need:
    - An SSH client installed on the computer you're connecting *from*, and;
    - An SSH server on the computer you're trying to connect *to*.

- An SSH server isn't a physical machine.
  - It's a program that runs as a background process, constantly checking if a client is trying to connect with it. 
  - It then authenticates the request.

- The most popular SSH client on Linux is the **OpenSSH Program**.

- A popular form of SSH for Windows is **PuTTY**.

- To log into a remote machine, you need to have an account on that computer.

- You also need the host name/IP address for that computer.

- You can connect through SSH using a password; but that's not the most secure method.

- Alternatively, you can use an **SSH authentication key**.
  - SSH keys come in a set of two keys: *private* and *public*
  - You can lock something with a public key; but you can only unlock it with a private key, and vice-versa. 
  - [Read more about SSH authentication keys]()

- Another method of secure remote connection is a **VPN**.
  - **Virtual private network (VPN):** Allows you to connect to a private network (like your work network) over the Internet.


### Remote Connections on Windows

- **PuTTY** is a free, open source software that you can use to make remote connections through several network protocols, including SSH.

- In PuTTY configuration, make note of the *host name, port,* and *connection type* options.
  - By default, the port is set to `22`, which is the default port the SSH protocol uses.

- PuTTY also comes with a tool called **Plink (PuTTY Link)**, which is implemented into the command line after PuTTY is installed (and used to make SSH connections).

- Microsoft provides another way to connect to other Windows computers with **Remote Desktop Protocol (RDP)** 
  = RDP clients are also available for Linux and Mac.
  - RDP provides a GUI.

- **Microsoft Terminal Services Client (MSTSC)** is used to create RDP connections to remote computers.


### Components of an Operating System

- **Operating system:** The whole package that manages our computer's resources and lets us interact with it.

- There are two main parts to an operating system: the **kernel** and the **user space**.
  - The **kernel** is the main core of an operating system: 
    - Directly communicates with the hardware;
    - Manages the system's resources;
    - Handles file storage and management.
  - And the **user space** is everything outside of the kernel (system programs, user interfaces, etc).

- The term *operating system* refers to both the kernel and user space.

#### The major operating systems dealt with in IT
- Windows (also commonly known as "PC")
- MacOS
- Linux
  - Ubuntu
  - Debian
  - Red Hat

- **Process management** is a kernel process that allows the computer to multitask at a rate faster than we can blink.

- The kernel optimizes *memory usage* and makes sure our applications have enough memory to run.

- **Input/Output (I/O) Management** is anything that can give us input, or that we can use for output of data.
  - It's how the kernel talks to external devices like discs, keyboards, audio devices, etc.
  - Clicking with your mouse is an example of this.

- In summary, main kernel operations are:
  - File management
  - Process management
  - Memory management
  - I/O management


### Files and File Systems

- There are 3 main components to handling files on an operating system
  1. File data
  2. Metadata
  3. File system

#### File system
- A brand new hard disk needs to be edited, so the OS needs to know what type of file system is used

- *NTFS* is the file system used by Windows, and is an evolution of the system introduced in Windows NT
  - NTFS features include encryption, faster access speeds, and superior security.
  - Windows is currently developing another file system called **ReFS (Refined File System)** but isn't ready for consumer use yet.

- **APFS** is the default file system for MacOS, as of March 2017.
  - Previously was HFS+. It's *journaled*, which means it does a better job saving your disk state in case of failure.

- Different Linux distributions use different file systems; but a standard for Linux is **ext4** (the fourth iteration of ext file systems, and backwards-compatible).

- A good rule of thumb is to stick with the file system that your operating system recommends.

#### Data
- We write data to our hard drive in the form of *data blocks*.
  - This mean data saved can be broken down into different pieces and written to different parts of the disk, instead of in one solid piece.

- **Block storage** improves faster handling of data because the data isn't stored as one long piece and can be accessed quicker. 
  - It also helps manage storage space.

- **Metadata** tells us everything we need to know about a file.
  - File owner
  - Permissions
  - File size
  - Date modified
  - Date created
  - File type (extension)

- **File extension** is the appended part of a filename that tells us what type of file it is in certain operating systems.

- A working knowledge of file systems (and the differences between them) can help you do things like recover data from damaged disks; or explore ways to boot from two different kinds of operating systems (like Windows or Linux) on the same computer.


### Process Management

- One of the most important kernel tasks is *process management*.

- **Process:** A program that's executing, like our internet browser or text editor.

- **Program:** An application that we can run, like Chrome.
  - When a program wants to run, a process has to be created for it.
  - This process requires hardware resources, like RAM and CPU.

- The kernel manages computer's resources effectively and efficiently. But technically, it doesn't handle everything *all at once*.
  - Instead, it executes processes one by one, through a method called a *time slice*.

- **Time slice:** A very short interval of time that gets allocated to a process for CPU execution.
  - So short you can't notice it. As in milliseconds.

- **Kernel:** Creates processes, efficiently schedules them, and manages how processes are terminated.
[Q: what does the kernel do?]

### Memory Management

- Memory is less plentiful than hard disk drive, so *virtual memory* is a way to generate more memory than the computer physically has.

- **Virtual Memory** is the combination of hard drive space and RAM that acts like memory that our processes can use.

[Pages stored in virtual memory]

- *"When we execute a process, we take the data of the program in chunks we call pages. We store these pages in virtual memory. If we want to read and execute these pages, they have to be sent to physical memory or RAM."*
  - Virtual memory stores pages that are currently not in use by physical memory.

- When virtual memory is stored on the hard drive, the allocated space is called *swap space*.

### I/O Management

- **I/O devices** are devices that perform input and output.
  - Includes monitors, speakers, mouse/keyboard, webcams, and hard disk drives.

- The kernel needs to be able to load drivers, so the computer can recognize and communicate with different types of hardware.

- The kernel also handles the transfer of data in and out of the devices.

- Devices also need to be able to talk to each other (like a webcam and microphone)

- The kernel handles all intercommunication between devices.

- *When you're troubleshooting or solving a problem with a slow machine, it's usually some sort of hardware resource deficiency.*
  - If you don't have enough RAM, you can't load up as many processes.
  - If you don't have enough CPU, you can't execute programs fast enough.
  - If you have too much input coming into the device--or too much output going somewhere--other data will be blocked from being sent or received.

- *"It's slow!"* Is one of the most common problems you'll solve as in an IT support role.

### Interacting with the OS: User Space

- There are two ways users can interact with the OS:
  1. Shell
  2. Graphical user interface (GUI)

- **Shell:** A program that interprets text commands and sends them to the OS to execute.

- A **GUI** is a visual way to interact with a computer, and implements much abstraction. 

- Some shells use a GUI, but IT professionals need to be familiar with the **command line interface (CLI) shell**.

- The most common shell is **BASH (Born Again Shell)**
  - The Windows shell is **Powershell**

### Logs

- **Logs** are files that record system events on our computer, just like a system's diary.

- Logs are kept so we can refer to them, when we need to find out something that happened.

### The Boot Process

- When you start up a computer, you use the term **boot**.

- **Booting** means to start from nothing, and follow a series of steps to arrive at a fully-operational system.

- A rundown of the boot process:
  1. The computer is powered on
  2. The BIOS/UEFI runs the **POST** to ensure the computer is in proper working order.
  3. A boot device is selected (hard drives, USB drives, or CD drives)
    - The computer then searches for a bootloader. 
  4. After a quick series of programs, the computer then loads the operating system.
  5. After the bootloader loads the operating system, the kernel gets loaded.
  6. The kernel allocates the computer's resources, loads drivers, and transfers data from hardware to software.
  7. Essential system processes and user space items are launched
    - Processes such as user login, desktop environments, etc.

- **BIOS/UEFI:** A low-level software that initializes our computer's hardware to make sure everything is good to go.

- **Bootloader:** A small program that loads the operating system.

### Mobile Operating Systems

- Mobile operating systems are optimized to use as little power as possible, by removing OS features that the device doesn't need.

- Mobile user interfaces (such as touch and voice) require adding device drivers and support to the mobile operating system.


## Installing an Operating System

### Choosing an Operating System

The operating systems in use by an organization have a lot to do with the applications and systems that they need to run.

- When choosing an operating system, ask:
  - Are you working with an organization or service that requires the use of a specific operating system?
  - What software will need to be run on this device?

  - What hardware will be used?

- Choose the operating system that matches your CPU
  - For example, a 64-bit operating system for a 64-bit processor.

- You can use different media for installing operating system (like disk or USB)
  - As an IT Support Specialist, you'll install an operating system many times, so using one single disk won't be time efficient or scalable. 

### Virtual Machines

- **Virtual machine (VM):** Just a copy of a real machine.

### Installing Windows

- Pretty straightforward.

### Installing Linux

- A host name should follow a certain standardization.
  - Username-Location (ex: cindy-nyc)

### What is Chrome OS?

- *Unlike other operating systems, Chrome OS has one main purpose: To be a secure and simple way for the user to interact with the web.*

The power of the web browser, and advancement in web browser applications, have legitimized an operating system centered around running a web browser. 

- Today, you can do many things through just a web browser:
  - Communicate through email
  - Create and share documents
  - Edit photos
  - Connect remotely to another computer

- Chrome can also run Android and Linux applications inside containers.

- Chrome's UI is set up so you only see the Chrome web browser's interface; but process management, memory, and input/output are still happening behind the scenes.

- When you log into a Chrome OS machine, you're also signing into the Chrome browser.

- *Chrome OS machines are interchangeable because most data is stored in the cloud, not locally.*

- Chrome users **don't** have administrator rights, and the OS has an auto-update feature. In other words, there's no meddling required by users.
  - The auto-update also includes a failsafe, in case things go wrong.
  - *This means that the user doesn't need to worry about problems or hacks in the system because it's designed to stay up and running.*
  - As a result, Chrome has powerful security.

---

## Questions for review

### Keywords
<details>
  <summary>What is a remote connection?</summary>
  <p>A remote connection allows us to manage multiple machines from anywhere in the world.</p>
</details>

<details>
  <summary>What is SSH?</summary>
  <p>Secure shell (SSH) is a protocol, implemented by other programs to securely access one computer from another.</p>
</details>

<details>
  <summary>What is VPN?</summary>
  <p>A virtual private network (VPN) allows you to connect to a private network (like your work network) over the Internet.</p>
</details>

<details>
  <summary>What is PuTTY?</summary>
  <p>A popular open-source SSH application for Windows.</p>
</details>

~

<details>
  <summary>What is an operating system?</summary>
  <p>The whole package that manages our computer's resources and lets us interact with it. It is composed of a kernel and a user space.</p>
</details>

<details>
  <summary>What is a kernel?</summary>
  <p>The kernel is the main core of an operating system.</p>
</details>

<details>
  <summary>What is a user space?</summary>
  <p>Everything outside of the kernel (system programs, user interfaces, etc).</p>
</details>

<details>
  <summary>What are the three major operating systems in IT?</summary>
  <p>Windows ("PC"), MacOS, and Linux (including Ubuntu, Debian, and Red Hat).</p>
</details>

<details>
  <summary>What is process management?</summary>
  <p>A kernel process that allows the computer to multitask at a rate faster than we can blink.</p>
</details>

<details>
  <summary>What is I/O management?</summary>
  <p>Input/output (I/O) management is anything that can give us input, or that we can use for output of data.</p>
</details>

~

<details>
  <summary>What is NTFS?</summary>
  <p>The file system used by Windows; evolved from the system introduced in Windows NT.</p>
</details>

<details>
  <summary>What is APFS?</summary>
  <p>The default file system for MacOS.</p>
</details>

<details>
  <summary>What is ext4?</summary>
  <p>The standard file system used by most Linux distributions.</p>
</details>

~

<details>
  <summary>What is block storage?</summary>
  <p>The breaking of data into smaller blocks, so they can be accessed quicker from the hard drive.</p>
</details>

<details>
  <summary>What is a file extension?</summary>
  <p>The appended part of a filename, which tells us what type of file it is in certain operating systems.</p>
</details>

~

<details>
  <summary>What is a process?</summary>
  <p>A program that's executing, like our Internet browser or text editor.</p>
</details>

<details>
  <summary>What is a program?</summary>
  <p>An application that we can run, like Chrome.</p>
</details>

<details>
  <summary>What is a time slice?</summary>
  <p>A very short interval of time that gets allocated to a process for CPU execution.</p>
</details>

~

<details>
  <summary>What is virtual memory?</summary>
  <p>The combination of hard drive space and RAM, that acts like memory that our processes can use.</p>
</details>

<details>
  <summary>What are I/O devices?</summary>
  <p>Devices that perform input and output.</p>
</details>

<details>
  <summary>What is a driver?</summary>
  <p>Drivers are programs that enable a computer to recognize and communicate with different types of hardware.</p>
</details>

~

<details>
  <summary>What is a shell?</summary>
  <p>A program that interprets text commands and sends them to the OS to execute.</p>
</details>

<details>
  <summary>What is a GUI?</summary>
  <p>A visual way to interact with a computer, implementing much abstraction.</p>
</details>

<details>
  <summary>What is BASH?</summary>
  <p>Born Again Shell (BASH) is the most common shell.</p>
</details>

~

<details>
  <summary>What are logs?</summary>
  <p>Files that record system events on our computer, much like a system's diary.</p>
</details>

<details>
  <summary>What does "booting" mean?</summary>
  <p>To start from nothing, and follow a series of steps to arrive at a fully-operational system.</p>
</details>

<details>
  <summary>What is the BIOS/UEFI?</summary>
  <p>A low-level software that initializes our computer's hardware to make sure everything is good to go. (UEFI is the successor of BIOS.)</p>
</details>

<details>
  <summary>What is a bootloader?</summary>
  <p>A small program that loads the operating system.</p>
</details>

~

<details>
  <summary>What is a virtual machine?</summary>
  <p>A copy of a real machine (usually, a copy of a computer and its operating system).</p>
</details>

### Concepts

<details>
  <summary>How do SSH authentication keys work?</summary>
  <p></p>
</details>

<details>
  <summary>What is the difference between RDP and MSTSC?</summary>
  <p></p>
</details>

<details>
  <summary>What are the two main parts of an operating system?</summary>
  <p></p>
</details>

<details>
  <summary>What are the main kernel operations?</summary>
  <p></p>
</details>

<details>
  <summary>What are the 3 main components of file management?</summary>
  <p></p>
</details>

<details>
  <summary>How do data blocks work?</summary>
  <p></p>
</details>

<details>
  <summary>What are the aspects of file metadata?</summary>
  <p></p>
</details>

<details>
  <summary>How do pages work in virtual memory?</summary>
  <p></p>
</details>

<details>
  <summary>What is a basic summary of the boot process?</summary>
  <p></p>
</details>
