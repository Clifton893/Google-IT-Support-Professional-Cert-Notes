# Week 4: Filesystems

## Filesystem Types

### Review of Filesystems

Recall that a **filesystem (fs)** is used to keep track of files and file storage on a disk.
- Without a filesystem, the operating system wouldn't know how to organize files.

Windows uses the NTFS filesystem; and Linux generally uses ext4. But these are not cross-operating.
- A USB drive using NTFS can be used by both Windows and Ubuntu Linux
- However, a USB drive using ext4 will only work on Ubuntu, not with Windows

Filesystems like **FAT32** support reading and writing data to all three major operating systems. 
- However, it doesn't support files larger than 4 GB
- And the size of the filesystem can't be larger than 32 GB


### Disk Anatomy

A **storage disk** can be divided into something called *partitions*.
- A **partition** is just a piece of the disk that you can manage.
- When you create multiple partitions, it gives you the illusion that you're physically dividing a disk into separate disks.

To add a filesystem to a disk, first you need to create a partition. Usually, we just have a single partition for our OS; but it's not uncommon to have multiple partitions for different uses.

When you format a filesystem on a partition, it becomes known as a **volume**. (Volume and partition are mistakenly used synonymously, so know that there is a difference.)

#### Partition Table
The other component of a disk is a *partition table.* 
- A **partition table** tells the OS how the disk is partitioned.
- The table will tell you which partitions you can boot from, how much space is allocated, etc

There are two main partition table schemes that are used: MBR, or GPT.

**Master Boot Record (MBR)** is a traditional partition table, mostly used in Windows OS. 
- It only lets you have volume sizes of 2 TB or less.
- It also uses something called *primary partitions*.
  - You can only have four primary partitions on a disk.
  - If you want to add more, you have to convert a primary partition into an *extended partition*
    - And inside the extended partition, you can make a *logical partition*
- MBR is an old standard, slowly being phased out by GPT.

**GUID Partition Table (GPT)** is becoming the new standard for disks.
- You can have a volume size greater than 2 TB;
- It has only one type of partition;
- And you can make as many of them as you want on a disk.
- UEFI (the emerging BIOS standard) requires the GPT.


### Windows: Disk Partitioning and Formatting a Filesystem

#### Through GUI

Windows ships with a native tool called Disk Management Utility.
- You can access it through the GUI, right-clicking on "This PC" to "Manage," then clicking "Disk Management"

Quick format vs. full format
- In a full format, Windows will do a little extra work to scan the disk or USB drive for errors or bad sectors
- This extra work will make the formatting process take longer

Enable vs. disable file/folder compression
- If you enable, your files and folders will take up less space on the disk;
- But compressed files will need to be expanded when you open them, which puts more work on the computer's processor

#### Through command line

Disk manipulation through the CLI can be done through Diskpart.
- **Diskpart** is a terminal-based tool built for managing disks right from the command line.
- To launch, open a command prompt, and run `Diskpart`
- This will open another terminal window, where the prompt reads `DISKPART>`
- You can list the current disks on the system by typing `list disk`


### Windows: Mounting and Unmounting a Filesystem

After you format a filesystem, you have to mount the filesystem to a new drive.

**Mounting** is making something accessible to the computer, like a filesystem or a hard disk.

Windows does this automatically. All you have to do is, when you're done using the drive, to safely eject (essentially, ummount) the drive.


### Linux: Disk Partitioning and Formatting a Filesystem

Linux has several partitioning command line tools; one that supports both MBR and GPT partitioning is the **Parted** tool. 

Parted can be used in two modes:
- Interactive, meaning we're launched into a separate program (like when we use the `less` command)
- Command line, meaning you just run commands while still in your shell.

To show what disks are connected to the computer, run `sudo parted -l`. This lists out the disks that are connected to our computer.
- The number field (in Parted) corresponds to the number of partitions on the disk. 
  - So the first partition will correspond to `/dev/sda1`, the second will be `/dev/sda2`, etc.
- The start field is where the partition starts on the disk.
  - For example, starting at 1,049 kilobytes and ending at 538 megabytes.
- The field after that shows how large the partition size is.
- The next field tells us what file system is on the partition.
- Then, the name.
- Finally, some flags that are associated with the partition.

The `mklabel` command sets a disk label to be recognized.

The `mkpart` command is used inside the Parted tool, and requires the following information:
- What type of partition you want to make;
- What file system you want to use;
- The start of the disk;
- And the end of the disk.

Partition type is only meaningful for MBR partition tables--remember that MBR uses primary, extended, and logical partitions.

Some operating systems measure one kilobyte as 1,024 bytes, even though that is actually a *kibibyte* and not a kilobyte. When dealing with data storage, you want to be as absolutely precise in measurement as you can be, so you don't waste precious memory space.

After this step, `quit` out of Parted, since you need to format the partition with the filesystem.
- Do this by running `sudo mkfs -t ext4 /dev/PARTITION`


### Linux: Mounting and Unmounting a Filesystem

To begin interacting with the disk, you need to mount the filesystem to the directory. But first, you need to create a directory on your computer, and then mount the filesystem to the directory.
- EX: `sudo mount /dev/sdb1 /my_usb/`

You can also unmount the filesystem using the `umount` command.
- When you shut down your computer, disks that were mounted manually are automatically unmounted.
- Always be sure to unmount a filesystem of a drive before physically disconnecting the drive.

You can permanently mount a disk if you need it to automatically load up when the computer boots.
- To do this, you need to modify a file called `/etc/fstab` ("filesystems table"). Inside, you'll see a list of unique device IDs, their mount points, what type of filesystem they are, and other information.
- The first field you'd need to add for `/etc/fstab` is the universally unique identifier (UUID) of the disk.
  - To get the UUID of your devices, you can run `sudo blkid`. 
  - This will show the UUID for block device IDs (aka storage device IDs).


### Windows: Swap

A relevant concept to disks and partitions is swap space. But before talking about swap space, let's review virtual memory.
- Recall that **virtual memory** is how our OS provides the physical memory available in our computers (like RAM) to the applications that run on the computer.
- It does so by creating a *mapping*, a virtual-to-physical address.
- This provides several benefits:
  - The program (which needs to access memory) doesn't have to worry about what portions of memory other programs might be using;
  - The program doesn't have to keep track fo where the data it's using is located in RAM;

Virtual memory also allows the computer to use more memory than it physically has installed.
- It does this by dedicating an are of the hard drive to use as a storage base, for blocks of data called *pages*.
- When a particular page of data isn't being used by an application, it gets evicted.
  - This means it gets copied out of memory, onto the hard drive.
  - This is because accessing data on RAM is much faster than the hard drive (where space is at a premium)
  - So, the operating system wants to keep the most commonly-accessed data pages in RAM;
  - And pages not used in a while are stored on the disk.
- A good analogy is that swap space is your pocket; and the hard drive is your backpack.

Windows provides a way to modify the size, number, and location fo paging files. This is done through the "System Properties" applet, in the Control Panel.


### Linux: Swap

In Linux, the dedicated area of the hard drive used for virtual memory is known as **swap space**.

- To make swap space, go into the Parted tool, and select where your storage device is.
- Partition it again, to make a swap partition.
- Then format the `linux-swap` filesystem on it.
- Swap isn't actually a filesystem, so it isn't done yet!
  - (Remember, pages go into swap, not file data.)
- Quit out of Parted, then run `sudo mkswap dev` with the location of the new swap partition.
- Lastly, run `sudo swapon` to the location, to enable swap on the device.

If you want to automatically mount swap space every time the computer boots up, just add a swap entry to the `/etc fstab` file.


### Windows: Files

Remember that the operating system manages file data, file metadata, and filesystems.
- When we talk about data, we're referring to the actual contents of the file (like a text document saved to hard drive).
- The file metadata includes everything else (like owner of the file, permissions, size of the file, location on hard drive, etc)

#### How does NTFS store and represent files?
- NTFS uses something called the **master file table (MFT)** to organize everything.
- Every file on a volume has at least one entry in the MFT (including the MFT itself)
  - Usually, there's a 1:1 correspondence between files and MFT records;
  - But if a file has many attributes, there might be more than one record to represent it.
  - Remember that attributes include file name, creation time stamp, its permission, compression, location, etc

When you create files on an NTFS filesystem, entries get added to the MFT.
- When files get deleted, their entries in the MFT are marked as *free* so they can get reused.

An important part of a file's entry in the MFT is an identifier called the **file record number**.
- This is the index of the file's entry in the MFT.
- A special type of file in Windows is called a *shortcut*
  - A shortcut is just another file and another entry in the MFT;
  - But it has a reference to some destination, so when run, it directs you to that destination.

Aside from creating shortcuts, NTFS provides two other ways to access other files, in hard and symbolic links.

**Symbolic links** are like shortcuts, but at the filesystem level.
- When you create a symbolic link, you create an entry in the MFT that points to the name of another entry/file.
- But unlike shortcuts, symbolic links are treated as substitutes for the file they're linked to in almost every meaningful way.

When you create a **hard link** in NTFS, an entry is added to the MFT that points to the linked file record number, not the name of the file.
- This means the file name of the target can change, and the hard link will still point to it.
- Since a hard link points out the file record number and not the file name, you can change the name of the original file and the link will still work.


### Linux: Files

In Linux, metadata and files are organized into a structure called an **inode**.
- Inodes are similar to the Windows NTFS MFT records.
- We store inodes in an inode table, and they help us manage the files on our file system.
- The inode itself doesn't actually store file date or file name; but it does store everything else about a file.

Shortcuts in Linux are referred to as **softlinks**, or **symlinks**. 
- They work in a similar way symbolic links work in Windows, in that they just point to another file.
- Softlinks allow us to link to another file using a file name;
- They're great for creating shortcuts to other files.
- To create a softlink, run the `ln` command with the `-s` flag for softlink.
  - So `ln -s FILENAME FILENAME_SOFTLINK`

The other type of links found in Linux are **hardlinks**.
- Similar to Windows, hardlinks don't point to a file;
- In Linux, they link to an inode, which is stored in an inode table on the file system.
- Essentially, when you creating a hardlink, you're pointing to a physical location on disk (more specifically, on the filesystem).
  - But if you deleted a file of a hardlink, all other hardlinks would still work.
- In the third field of file details, the field actually indicates the amount of hardlinks a file has.
  - When the hardlink count of a file reaches zero, then the file is completely removed from the computer.
- To create a hardlink, run the `ln` command to specify a hardlink.
  - So `ln FILENAME FILENAME_HARDLINK`

Hardlinks are great if you need to have the same file stored in different places, but you don't want to take up any additional space on the volume. (Better than softlinks, since those can be broken.)


### Windows: Disk Usage

To check disk usage, open up the Computer Management utility; then go to the Disk Management console; and right-click on the partition you're interested in and click "Properties."

The "Disk Cleanup" button will launch a program called `cleanmanager.exe`, which performs housekeeping tasks such as deleting temporary files, compressing old/rarely-used files, cleaning up logs, and emptying the recycle bin.

The command line disk usage utility can be useful for creating scripts (which may need text-based output instead of visual reports in the GUI).

Another task related to disk health is called **defragmentation**.
- The idea behind disk defragmentation is to take all the files stored on a given disk, and reorganize them into neighboring locations.
- Having files ordered like this will make it easier for hard drive disks, which use an actuator arm to write to and read from a spinning disk.
  - The head of the actuator arm will actually travel less to read the data it needs.
- This is less of a benefit for solid state drives, since there is no physical read/write head that moves around a spinning disk.
- Defragmentation is a regularly-scheduled task in Windows.
  - To manually defragment, open up the Disk Defragmenter tool bundled with Windows.

Instead, for SSD drives, the operating system can use a process called **trim** to reclaim unused portions of the solid state disk.


### Linux: Disk Usage

In Linux, you can view disk utilization on your computer with the `du -h` command.
- The `du`, or "disk usage" command, shows the disk usage of a specific directory.
  - If you don't specify a directory, it'll default to your current one.
- The `-h` flag gives you the data measurements in "human readable" form.
- You should use the `du` command if you want to know how much data space is being used by files in a directory.

Another command you can use if you want to know how much free space you have on your machine is the `df`, or "disk free" command.
- This shows you the free space available on your entire machine.
- Again, the `-h` flag presents you the data measurements in human readable form.
- You should use the `df` command if you want to know how much free space you have on your entire system.

Linux generally does a better job of avoiding fragmentation than Windows does.


### Windows: Filesystem Repair

When we read or write something to a drive, we actually put it into a buffer, or cache, first.
- A **data buffer** is a region of RAM that's used to temporarily store data while it's being moved around.
  - So when you copy something from your OS to your USB drive, it first gets copied to a data buffer because RAM operates faster than hard drives.

If you don't properly unmount a filesystem and give your buffer enough time to finish moving data, you run the risk of data corruption.

NTFS has several advanced features included to help minimize the danger of corruption (as well as try to recover damaged files).
- One such feature, through a process called *journaling*, logs changes made to a file's metadata into a log file, called the NTFS log.
  - By logging these changes, NTFS creates a history of the actions it's taken; meaning it can look at the log to see what the current state of the file system should be.
- In addition to journaling, NTFS implements *self-healing*.
  - This mechanism makes changes to minor problems and corruptions on the disk automatically in the background
  - It does this while Windows is running, so you don't need to perform a reboot.
- To check the status of the self-healing process, open an administrative command prompt;
  - Then run the `fsutil repair query DRIVE`

### Linux: Filesystem Repair

To repair a filesystem manually in Linux, you can use `fsck`, the file system check command.
- Ex:`sudo fsck /dev/sdb`

*Don't run* `fsck` *on a mounted partition*, as there's a high chance it will damage the filesystem.

