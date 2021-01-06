# Week 5: Data Recovery & Backups

## Planning for Data Recovery

### What is Data Recovery?

**Data recovery** is the process of trying to restore data after an unexpected event that results in data loss or corruption.

When an unexpected event occurs, your main objective is to resume normal operations as soon as possible, while minimizing the disruption to business functions.

The best way to be prepared for a data-loss event is to have a well-thought-out disaster plan and procedure in place.

Disaster plans should involve making regular backups of any and all critical data that's necessary for your ongoing business processes.

A **post-mortem** is a way for you to document any problems you discovered along the way; and most importantly, the ways you fixed them so you can make sure they don't happen again.


### Backing Up Your Data

Data you'll want to back up includes (but is not limited to):
- Email databases
- Sales databases
- Financial spreadsheets
- Server configurations
- Databases

#### Local storage
- Pros:
  - Data is physically nearby
  - Low bandwidth needs
- Cons:
  - Data loss due to damage at location

#### Off-site storage
- Pros:
  - Data is safer in multiple locations
- Cons: 
  - Needs security and encryption
  - Needs large amounts of bandwidth


### Backup Solutions

On-site/self-managed backups could be as simple as buying a commercial NAS device, loading it with a bunch of hard drives, and sending data to it over the network. Long term, this is not an optimal solution, however.

If your organization's budget allows, you should have on-site and off-site backups.

The standard medium for archival backup data storage is data tapes. They're much like audio cassette tapes, since they use spools of magnetic tape run through machines that allow data to be written to -- and read back from -- the tape.

**rsync** isn't explicitly a backup tool, but it's very commonly used as one. 
- It's a file transfer utility, designed to efficiently transfer and synchronize files between locations or computers.
- rsync supports compression
- You can use SSH to securely transfer data over a network
- Using SSH, it can also synchronize files between remote machines, making it useful for simple, automated backups.


Apple has a first-party backup solution, called **Time Machine**.
- It operates using an incremental backup system.

Microsoft offers a first-party solution called **Backup and Restore**. It has two modes of operation:
- A file-based version, where files are to a zip archive
  - Supports either complete backups or incremental ones;
- The system image, where the entire disk is saved block by block to a file
  - Supports differential mode, only backing up blocks on the disk that have changed since the last backup.


### Testing Backups

It's not sufficient just to set up regular backups -- you also need a recovery process, and that process needs to be tested regularly.

**Restoration procedures** should be documented and accessible so that anyone with the right access can restore operations when needed.

**Disaster recovery testing** involves documenting the procedure, regularly testing the documentation to ensure it works (now and in the future), and is a critical exercise that should happen once a year or so.


### Types of Backup

Ways to perform regular backups:
- Full backup
  - 
- Differential backup
  - 
- Regular incremental backups
  - 

While a differential backup backs **up** files that have been changed or created **since the last full backup**, an incremental backup is when only the data that's changed in files **since the last incremental backup** is backed up.

It's a good practice to perform infrequent full backups, while also doing more frequent differential backups.

Another thing backup systems can do to help save space is **file compression**.
- When creating a backup, all the files and folder structures will be copied and put into an archive.
  - Archives are useful for keeping files organized and preserving full structure.
- Compression is a mechanism of storing the same data while requiring less disk space, by using complex algorithms.

To store backup data on site, you can use a commercial NAS device; or configure a file server with a large amount of disk space.

**Redundant Array of Independent Disks (RAID)** is a method of taking multiple physical disks and combining them into one large virtual disk.
- RAID arrays are a great, inexpensive way of creating a lot of data capacity, while minimizing risk of data loss in the event of disk failure.
- They can also be flexible enough to allow future growth in disk capacity.

*RAID isn't a backup solution; it's a *data storage* solution.* A RAID array doesn't protect against accidentally deleting files, or malware corrupting your data. *RAID is not a replacement for backups.*


### User Backups

Ensuring reliable backups for client devices is a bit more challenging than infrastructure devices.

One common solution to user backups is to use a cloud service, such as Dropbox, Apple iCloud, and Google Drive.


## Disaster Recovery Plans

### What's a Disaster Recovery Plan?

A **disaster recovery plan** is a collection of documented procedures and plans on how to react and handle an emergency or disaster scenario, from the operational perspective.

The goal of the disaster recovery plan is to minimize disruption to business and IT operations, by keeping downtime of a system to a minimum and preventing significant data loss.

The plan actually covers preventive measures and detection measures, on top of the post-disaster recovery approach.

**Preventative measures** cover any procedures or systems in place that will proactively minimize the impact of a disaster. (This includes things like regular backups and redundant systems/power supplies.)

**Detection measures** are meant to alert you and your team that a disaster has occurred that can impact operations.

Other things that should be monitored to help head off any unexpected disasters include:
- Environmental sensors
- Flood sensors (in the server room)
- Temperature and humidity sensors (in the server room)
- Evacuation procedures

**Corrective or recovery measures** are those enacted after a disaster has occurred. (These measures involve steps like restoring lost data from backups or rebuilding and reconfiguring systems that were damaged.)

When one system in a redundant pair suffers a failure, it's called a **single point of failure.**


### Designing a Disaster Recovery Plan

- Perform Risk Assessment
  - A **risk assessment** allows you to prioritize certain aspects of the organizations that are more at risk if there's an unforeseen event.
- Determine Backup and Recovery Systems
  - Anything critical to operations should be made redundant whenever possible.
- Determine Detection & Alert Measures & Test Systems
- Determine Recovery Measures


## Post-Mortems

### What's a post-mortem?

- We create a **post-mortem** after an incident, an outage, or some event when something goes wrong, or at the end of a project to analyze how it went.
- The purpose of a most-mortem is to learn something from an event or project, not to punish anyone or highlight mistakes.


### Writing a post-mortem

- A typical post-mortem for an incident begins with a brief summary (just a short paragraph)
  - What the incident was
  - How long it lasted
  - What the impact was
  - How it was fixed
- Always clearly state the timezone to be clear while listing dates and times.
- Next is a detailed timeline of key events
  - The timeline should wrap up with the actions taken that resolved the outage and restored services, signaling the end of the event.
- Next, a very detailed and honest account of the root cause is covered.
  - What led to the issue
- A more detailed explanation of the resolution and recovery efforts should be documented next.
- Lastly, close out the report with a list of specific actions that should be taken to avoid the same scenario from happening again.

Analyzing *what went well* is just as important as what went wrong. Highlight failsafes and effectiveness of the system in place.
