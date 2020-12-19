# Week 3: Package and Software Management

## Software Distribution

### Windows: Software Packages

- In Windows, software is usually packaged as a `.exe` (executable file)
- **Executable files (.exe)** contain instructions for a computer to execute when they're run.
  - They're created according to Microsoft's *portable executable (PE) format*.
  - They include instructions for the computer to perform, text, computer code, images, and possibly an `.msi file`.
- A **Microsoft install package (.msi)** is used to guide a program--called the *Windows Installer*--in the installation, maintenance, and removal of programs on the Windows operating system.
  - Besides using the GUI setup *wizard* to guide the user in installation, the Windows Installer also uses the .msi file to create instructions on how to remove the program, if so desired.

Executables can simply contain a .msi file; or they can be used as stand-alone, custom installers without .msi or use of the Windows Installer.
  - For precise, granular control over the actions Windows takes when installing software, a custom installer may be better.
  - But while Windows Installer has strict rules about how software gets installed, it does handle a lot of the setup and bookkeeping for you.

As of Windows 8, Microsoft introduced a platform to distribute programs, called the Windows Store (later renamed the **Microsoft Store**). 
- The store is an application repository (or warehouse), where you can download and install universal Windows platform apps.
- These programs use a format called **APPX** to package their contents and act like a unit of distribution.


### Linux: Software Packages

There are many different Linux distributions, each with different package types.
- For example, Red Hat uses `.rpm` (Red Hat Package Manager) packages.
- Ubuntu uses **Debian** packages.
  - **Debian** packages as a `.deb` file for Debian Linux (on which Ubuntu is based)

- To install a Debian package, you'll need to use the `dpkg` ("Debian package") command.
  - Ex: `sudo dpkg -i SOFTWARE.deb`
- You can list the Debian packages installed on your machine with `dpkg -l`
- Or, you could search for and list them with `dpkg -l | grep SOFTWARE`


### Mobile App Packages

- Software for mobile operating systems is distributed as *mobile applications*, or *apps*.
- Mobile OS also require their apps to come from a source the device has been configured to trust--an app store.
- **App stores** are a central, managed marketplace for app developers to publish and sell mobile apps.
  - The **App store app** acts like a package manager;
  - The **App store service** acts like a package repository
  - Apps published through an app store are signed by the developer; and an OS is configured to only trust code that's been signed by publishers it recognizes.

**Enterprise app management** allows an organization to distribute custom mobile apps, developed by and for the organization and unavailable to the general public.
- Enterprise apps are signed with an enterprise certificate that has to be trusted by the device installing the application.

**Side-loading** is where you install mobile apps directly, without using an app store.
- Side-loading packages is riskier than installing through an app store
- You would generally only do this if you're an app developer

Mobile apps are standalone software packages, so they contain all their dependencies.

Mobile apps are assigned a specific storage location for their data.
- Anything that's changed or created with that app will end up in that app's assigned storage location, aka **cache**.
- So a mobile app factory reset is as simple as deleting/clearing the cache.


### Windows: Archives

An **archive** is comprised of one or more files that's compressed into a single file.

**Package archives** are the core or source software files that are compressed into one file.

When we install software from a source archive, it's referred to as *installing from source*.

Popular archive types you'll see include `.tar`, `.zip`, and `.rar`.
- To install software found in an archive, you first have to extract the contents of the archive (so you can see the files inside)


**7-zip** is a popular open-source tool for archiving and unarchiving different file types.


### Linux: Archives

7-Zip is also available for Linux. You can extract a file with it, using the `7z -e FILE` command.

Among the many archival tools, one already installed on most Linux distros is the `tar` command.


### Windows: Package Dependencies

**Having dependencies** is counting on other pieces of software to make an application work, since one bit of code depends on another, in order to work.

A **library** is a way to package a bunch of useful code that someone else wrote.
- This code is bundled together into a single unit.
  - Programs that want to use the functionality that the code provides can tap into it if they need to.
- In Windows, these libraries are called **dynamic-link libraries (DLL)**

The same DLL can be used by lots of different programs; it doesn't need to be loaded into memory for each application that wants to use it. Thus, less overall memory is used.

#### SxS
Most shared libraries and resources in Windows are managed by something called **side-by-side assemblies**, or **SxS**.
- Most of these shared libraries are stored in a folder at `C:\Windows\WinSxS`
- If an application needs to use a shared library to perform a task, that library will be specified in something called a **manifest**.
  - This tells Windows to load the appropriate library from the SxS folder. 
- SxS also supports access to *multiple versions of the same shared library* automatically.

You can locate software and its dependencies directly from the command line through PowerShell's `Find-Package` cmdlet.

> A **cmdlet** is basically the name we give to Windows PowerShell commands that use the `verb-noun` format.


### Linux: Package Dependencies

Know that if you install a standalone package, you won't automatically install its dependencies.

**Package managers** come with the works to make package installation and removal easier, including installing package dependencies.



## Package Managers

### Windows: Package Manager

A **package manager** makes sure that the process of software installation, removal, update, and dependency management is as easy and automatic as possible.

> `apt` is actually a package manager for the Ubuntu operating system.

**Chocolatey** is a third-party package manager for Windows.
- It's not written by Microsoft
- It lets you install Windows applications from the command line
- It's built on existing Windows technologies like PowerShell
- It lets you install any package or software that exists in the public Chocolatey repository


### Linux: Package Manager Apt

The **Advanced Package Tool** `apt` is used to extend the functionality of the package.
- It makes package installation easier
- It installs package dependencies for us
- Makes it easier for us to find packages that we can install
- It cleans up packages we don't need
- And more!

`apt` grabs the dependencies that a package requires automatically, and asks if you want to install it.

With a *package repository*, you don't have to manually search for each and every software you want online.

**Repositories** are servers that act like a central storage location for packages.
- You can add a software's link to your own machine, so it references that package or list of packages
  - An example is the `Register-PackageSource` cmndlet in PowerShell
  - In Ubuntu, the repository source file is `/etc/APT/sources.list`
- In Linux, there are also special repositories called PPAs:
  - A **Personal Package Archive (PPA)** is a software repository for uploading source packages to be built and published as an **Advanced Packaging Tool (APT)** repository by Launchpad.
    - Launchpad is a website owned by Canonical Limited, and its servers host PPAs.
  - Use caution when using a PPA instead of the original developer's repositories. 
    - The software can be defective, or even malicious.

You can update your package repositories with the `apt update` and `apt upgrade` commands.
- `apt update` updates the list of packages in your repositories, fetching the latest software available
  - But it won't install or upgrade, which means you need to use...
- `apt upgrade` will install any outdated packages for you automatically

You can use the `apt --help` command to learn more about the commands available with APT. 


## What's happening in the background?

### Windows: Underneath the Hood

When you click on an installation executable, what happens next depends on how the developer of the program has set their application app to be installed.

- If the `.exe` contains code for a custom installation that doesn't use the Windows installer system, then the details of what happens under the hood will be mostly unclear.
- Although you can't read the instructions the developer has written, you can use certain tools to check out the actions the installer is taking.
- The **Process Monitoring** program provided by the Microsoft CIS internals toolkit is one such way.
  - The program shows you any activity the installation executable is taking, like the files it writes and any process activity it performs.

#### MSI Files
- MSI files are closed source, so you won't be able to peek at the source code.
- MSI files are a combination of databases that contain installation instructions in different tables along with all the files, objects, shortcuts, resources, and libraries the program will need all grouped together.
- The Windows installer uses the info stored on the tables in the MSI database, to guide how the installation should be performed.
- Windows installer keeps track of all action it takes, and creates a separate set of instructions to undo them (this is how you can easily uninstall the program)

**Orca**, or `orca.exe` is a tool that Microsoft provides. It's part of the Windows software development kit (SDK), and helps you edit or create Windows installer packages.


### Linux: Underneath the Hood

Linux installs software directly from source code, so the process is far more straightforward than in Windows.
- A setup script is a script file that will run a bunch of tasks on the computer in order to set up the package.
  - A sample script can contain program instructions that compile code into machine instructions, compile binary to `/bin` directory, or create a folder to `/home/`, etc
- The README is a standard file contained in source archives, which has information about the archive.


## Device Software Management

### Windows: Devices and Drivers

Remember that a **driver** is used to help our hardware devices interact with our operating system.

In Windows, Microsoft groups all of the devices and drivers on the computer together in a single Microsoft management console called the **Device Manager**.

- Windows uses the **Plug and Play (PnP)** system, to automatically detect new hardware, which it then identifies and installs the appropriate software to manage it.
- Most vendors or computer hardware manufacturers will assign a special string of characters to their devices called a **hardware ID**.
- When Windows notices that a new device has been connected, the first thing it will do is ask the device for its hardware ID.
  - Once Windows has the hardware ID of the new device, the OS uses that ID to search for the right driver for the device.
  - It looks in a few places for the driver; starting with a local list of well-known drivers, then going onto Windows Update or the Driver Store.


### Linux: Devices and Drivers

- In Linux, everything is considered a file, even hardware devices.
- When a device is connected to the computer, a device file is created in the `/dev` directory.
  - This directory contains many devices, but not all of them are actual physical devices.
- **Character devices**, like a keyboard or mouse, transmit data character by character.
- **Block devices**, like USB drives, hard drives, and CD-ROMs transfer blocks of data.

Remember that the first bit you see in a `ls -l` command is the type of file. Among these are:
- `-` for regular file
- `d` for directory
- `b` for block device
- `c` for character device

Some files start with `/dev/sda` or `/dev/sdb`. SD devices are mass storage devices like hard drives, memory sticks, etc. 
- The A after SD just means the device was detected by th ecomputer first
  - So you could see `sda`, `sdb`, `sdc`, etc

#### Device Drivers
- Device drivers aren't stored in the `/dev` directory; sometimes they're part of the Linux kernel.
- A lot of modern hardware support is built into the kernel; so that when you plug in a device, it automatically works.
- But if there are devices that don't have support built into the kernel, they most likely have something called a **kernel module**.
  - A kernel module extends the kernel's functionality, without the developer actually touching the kernel (an intimidating prospect for many developers)
  - Not all kernel modules are drivers.
  - If you need to install a kernel module for a specific type of device, you can install it the same way you install all other software in Linux.


### Windows: Operating System Updates

A **security patch** is software that's meant to fix up a security hole.

The Windows Update Client service runs in the background on your computer to download and install updates and patches for your operating system. It does thsi by checking with the Windows Update servers at Microsoft, periodically.

As of Windows 10, Windows updates in a cumulative way. Every month, a package of updates and patches is released that supersedes the previous month's updates.


### Linux: Operating System Updates

Linux keeps its operating system up to date through updating the kernel.

- To view which kernel version you have, run `uname -r`
- To update the kernel and other packages, run `sudo apt update` and `sudo apt upgrade`
