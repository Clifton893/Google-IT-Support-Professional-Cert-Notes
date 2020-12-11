# Week 2: Users and Permissions

## Users and Groups

### Users, Administrators, and Groups, Oh My!

There are two different types of users:
1. **Standard users**
    - One who is given access to a machine but has restricted access to do things like install software or change certain settings.
2. **Administrators**
    - A user that has complete control over a machine.

Users are put together in **groups** according to levels of access and permissions to carry out certain tasks. 
- These tasks depend on what the computer's administrator deems to be appropriate.
- An administrator could give different access and settings based on the type of group a user is in.


### Windows: View User and Group Information

To view user and group information in Windows, use the Computer Management tool/application. 
- All of the essential settings that administrators need to change are found in the Computer Management tool.
- In an enterprise environment, you can manage multiple machines in something called a domain.
  - A **Windows domain** is a network of computers, users, files, etc that are added to a central database.

#### Computer Management (tool)
Underneath this menu, we have System Tools:
- Task Scheduler
  - This lets you schedule programs and tasks to run at certain times (like automatically shutting off the computer at 11:00pm every night)
- Event Viewer
  - This is where our system stores its system logs.
- Shared Folders
  - This shows the folders that different users on the machine share with each other.
- Local Users and Groups
  - This is where we'll be doing our user and group management.
- Performance
  - This shows monitoring for the resources of our machines (like CPU and RAM)
- Device Manager
  - This is where we go to manage devices to our computer like our network cards, sound cards, monitors, and more.
- Storage
  - A submenu for Disk Management.
- Services and Applications
  - This shows us the programs and services that we have available on the system (such as enabling/disabling DNS).

- **User access control (UAC)** is a feature in Windows that prevents unauthorized changes to a system.
  - These changes must be authorized by an administrator, instead.


### Linux: Users, Superusers, and Beyond

Linux has a few differences from Windows in how it labels users:
- Standard users
- Administrators
- Root user

#### Root User
- This is the first user that gets automatically created when a Linux operating system is installed.
- This user has all the privileges on the OS -- the superuser.
- Technically, there is only one superuser or root account;
  - But anyone granted access to use these powers can be called a superuser too.
- Logging in as root is dangerous; 
  - Instead, you can tell the shell you want to run just a single command as root. (Similar to Windows UAC.)
  - This is done with `sudo`, "superuser do"

#### Viewing memberships
You can see who has access to using `sudo` by viewing the `/etc/group` file, as well as viewing memberships for all groups.

Each user line has four fields (separated by colons):
1. The first field is the group name
2. The second field is the group password, usually an encrypted `x`
3. The third field is the group ID
4. The last field is a list of users in the group

**If you want to view the users on the machine**, the file is stored in `/etc/password`, not `/etc/user`.
- In this file, the first three fields (for each user) have significance:
  1. Username
  2. Password (again, encrypted)
  3. User ID (UID)
    - Root has a UID of zero.


### Windows: Passwords

If you're managing other people's accounts on a machine, you shouldn't know what their password is. Instead, you want the user to enter the password themselves.

#### Resetting a password
You can reset a password with Windows's Computer Management tool.
- Under "Local Users and Groups," right-click on a username; then click on "Properties."
  - Then, check the box for "User must change password at next logon."

You can also set a password for them manually, by right-clicking and selecting "Set password." But this isn't the best idea, and there are caveats (like using access to certain credentials).

To change a local password in PowerShell, you can use the DOS-style `net` command. (There is a native PowerShell command to do this, but it requires some scripting.)

`net` does many things, and changing local user passwords is one of them.
  - Since it's an old DOS command, you can use the `/?` parameter to get help in the CLI.
- To change a password for a user, the command is `net user USERNAME 'password'`
  - But the best way to do this is to use an asterisk `*` instead of writing the password out on the command line.
  - Using an asterisk will pause the command and prompt you to enter your password.
  - This is superior, because it maintains privacy;
    - Commands run on machines are usually recorded in a log file, that's sent to a central logging service
    - Thus, password secrecy is compromised
- But it's still best to keep other users' passwords private, even if you're an admin;
  - So instead, run ``net user USERNAME /logonpasswordchg:yes`


### Linux: Passwords
To change passwords in Linux, all you need to do is run the `passwd` (the password command).

If you're managing a computer and want to force a standard user to change their password, you can use the `-e` ("expire") flag with the command: `sudo passwd -e USERNAME`


### Windows: Adding and Removing Users

Adding a new user through the GUI is as simple as right-clicking and selecting "New User."
- Then you can set the username, full name, and password
  - You can also force the user to change their password at their next logon

In PowerShell, you can use `net user username * /add` to create a new user; but this will let you set their password credentials. So amend this with `net user USERNAME /logonpasswordchg:yes`
- Or combine the commands:
  - `net user USERNAME pa5sw0rd /add /logonpasswordchg:yes`

Deleting a user through the GUI is likewise a simple right-click affair.

In PowerShell, you can remove a user through the command `net user USERNAME /del`


### Linux: Adding and Removing Users

- To add a new user in Linux, run the command `sudo useradd USERNAME`
  - This will set up basic configurations for the user, and set up a home directory.
- Combine it with the password command to make them change their password, for better practice.
- To remove a user, simply run `sudo userdelete USERNAME`


### Mobile Users and Accounts

- In mobile devices, the initial account that you use during setup is called the *primary account*
  - This account is used to create a user profile for you on the device
- The user profile is like your user account in a mobile device, containing accounts, preferences, and apps.

**Single sign-on (SSO)** means apps will allow you to authenticate using an account that you're already signed into (such as iOS or Android accounts).

- Some smartphones use fingerprint sensors, facial recognition, or other kinds of biometric data to grant access to the device.
  - **Biometric data** is something about you that's unique to you, like a fingerprint, voice, or face.

**Mobile device management (MDM)** systems are used by organizations to protect business data, and are used to apply and enforce rules about how the device has to be configured and used.


## Permissions

### Windows: File Permissions

In Windows, files and directory permissions are assigned using **Access Control Lists (ACLs)**. One such type are **Discretionary Access Control Lists (DACLs)**.

Windows files and folders can also have **System Access Control Lists (SACLs)** assigned to them. SACLs are used to tell Windows that it should use an event log to make a note of every time someone accesses a file or folder.

#### Discretionary Access Control Lists (DACLs)
- A DACL is like a note about who can use a file, and what they're allowed to do with it.
- Each file/folder will have an owner, and one or more DACLs.

There are multiple DACL permissions you can assign to each user group:
- Read
  - Lets you see that a file exists, and allows you to read its contents.
  - It also lets you read the files and directories in a directory.
- Read and Execute
  - Lets you read files, and if the file is an executable, you can run the file.
  - R&E includes Read, so if you select this option, Read will automatically be selected, too.
- List folder contents
  - An alias for Read & Execute on a directory (checking one will check the other)
  - Means you can read and execute files in that directory
- Write
  - Lets you make changes to a file
  - You can have write access to a file without having read permission to that file
  - Also lets you create subdirectories, and write to files in the directory
- Modify
  - An umbrella permission that includes read, execute, and write
- Full control
  - A user or group with full control can do anything they want to the file!
  - Includes all of the permissions of Modify, and adds the ability to take ownership of a file and change its ACLs


### Linux: File Permissions

There are three different permissions you can have in Linux:
1. Read
  - This allows someone to read the contents of a file or folder.
2. Write
  - This allows someone to write information to a file or folder.
3. Execute
  - This allows someone to execute a program.

In the command line, the permission column is represented by 10 bits.
- The first is the file type (a `-` means the file is just a regular file; a `d` represents a directory)
- The next 9 bits are the actual permissions, grouped in sets of three (trios):
  - The first trio refers to the permission of the owner of the file
  - The second trio refers to the permission of the group that this file belongs to
  - The last trio refers to the permission of all other users
- `r` stands for "readable," `w` stands for "writable," and `x` stands for "executable"
- Like in binary, if a bit is set, then we say that it's *enabled*.
  - If a bit is a dash, it's *disabled*; if it's anything other than a dash, it's enabled


### Windows: Modifying Permissions

When using `icacls`, surround its parameters in single quotes (when using PowerShell.exe); when running in command.exe, you'll need to remove the single quotes for them to work.

#### Guest users
- This is a special type of user that's allowed to use the computer without a password. 
- Guest users are disabled by default. 
- You might enable them in very specific situations.

*Authenticated Users* are users with password credentials, unlike Guest Users.


### Linux: Modifying Permissions

Permissions are changed in Linux through the `chmod`, or "change mode" command.

#### Symbolic Format
- `u` the file/directory owner
- `g` the group the file belongs to
- `o` all other users

To add or remove permissions, just use a `+` or `-` to indicate who the permission affects.

#### Numeric Format

| Permission | Symbolic | Numeric |
|:----------:|:--------:|:-------:|
|    read    |     r    |    4    |
|    write   |     w    |    2    |
|   execute  |     x    |    1    |

- Add the numbers together to represent the permissions.
- Example: `chmod 754 my_cool_file`
  - The first number (7) is the owner's permission, which is read+write+execute
  - The second number (5), is the group's permission, which is read+execute
  - The third number (4) is all other users, which is read only.


### Windows: Special Permissions

Most of the permissions covered [in these notes] so far are *simple permissions*.

**Simple permissions** are actually sets of special, or specific permissions.
- For example, when you set the Read permission, you're actually setting multiple special permissions.

Usually, simple permissions will get the job done. But, sometimes you need to create a file or folder with special directories.

Some `icacles` permissions you can set:
- `WD` Write Data/Create Files
- `AD` Append Data/Create Folders
- `S` Synchronize

NTFS DACLs can be complicated, but it can also let you create really powerful sets of permissions customized to your exact needs.


### Linux: SetUID, SetGID, Sticky Bit

The **SetUID** bit is used to allow a file to be run as the owner of the file.
- The symbolic bit is a `s` and the numeric bit is a `4`

The **sticky bit** allows the file to be modified by anyone, but only removed by the owner or root.
- The symbolic bit is a `t` and the numeric bit is a `1`
