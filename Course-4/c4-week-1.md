# Week 1: Introduction to System Administration and IT Infrastructure Services

## What is System Administration?

**System administration** is the field in IT that's responsible for maintaining reliable computer systems in a multi-user environment.

System administrators -- or sysadmins -- have a diverse set of roles and responsibilities:
- Configuring servers;
- Monitoring the network;
- Provisioning/setting up new users in computers;
- And much more, handling many different things to keep an organization's IT infrastructure up and running.

**IT infrastructure** encompasses the software, the hardware, network, and services required for an organization to operate in an enterprise IT environment.


### Servers Revisited

A sysadmin is responsible for their company's IT services. These services include email, file storage, running a website, and are required so the company can be productive. And these services are all stored on servers.

A **server** is software or a machine that provides services to other software or machines.
- For example, a web server stores and serves content to clients through the Internet
- An email server provides email service to other machines
- An SSH server provides SSH services to other machines

Clients request the services from a server; and the servers respond with the services.

Server hardware can come in many different forms:
- They can be towers, similar to desktops
- Rack servers lay flat, are usually mounted in server racks, and provide multiple servers
- Blade servers are slim racks that stand upright, and provide even more storage space

#### KVM Switch
-KVM stands for "keyboard, video, & mouse"
- A KVM switch looks like a hub you can connect multiple computers to, and control them using one keyboard, mouse, and monitor.


### The Cloud

**Cloud computing** is the concept that you can access your data, use applications, store files, etc, from anywhere in the world; as long as you have an Internet connection.

"The cloud" isn't a magical thing--it's just a network of servers that store and process our data, via a data center.

A **data center** is a facility that stores hundreds or thousands of servers.

You could manage your own servers, or you could use data centers to manage your servers. Drawbacks of managed services include cost and dependency.

You might want to back up data on the cloud or a physical disk.


## Systems Administration Tasks

### Organizational Policies

In a small company, it's usually a sysadmin's responsibility to decide what computer policies to use.

A few common policy questions include whether users should be allowed to install software, require complex passwords, or view non-work related websites.


### User and Hardware Provisioning

Sysadmins have to be able to create new users and give them access to company resources; they also have to remove users from an IT infrastructure if users leave the company.

- Sysadmins are also responsible for user machines.
- They have to make sure a user is able to log in, and the computer has the necessary software that a user needs to be productive.
- Sysadmins also have to ensure that the hardware they are *provisioning* -- or setting up for users -- is standardized in some way.

Sysadmins also have to figure out the hardware lifecycle of a machine:
- When was it built?
- When was it first used?
- Did the organization buy it brand-new, or was it used?
- Who maintained it before?
- How. many users have used it in the current organization?
- What happens to this machine if someone needs a new one?

#### 4 Main Stages of Hardware Lifecycle
- **Procurement:** This is where hardware is purchased or reused for any employee;
- **Deployment:** This is where hardware is set up so that the employee can do their job;
- **Maintenance:** This is the stage where software is updated and hardware issues are fixed if and when they occur; 
- **Retirement:** This is the final stage, where hardware becomes unusable or no longer needed, and must be properly removed from the fleet.

An example of a typical hardware lifecycle:
- A new employee is hired by the company, and you're instructed to provision a computer;
- You allocate a computer you have from your inventory, or you order a new one;
- When you allocate hardware, you may need to tag the machine to keep track of which inventory belongs to the organization;
- Next you image the computer with the base image, preferably using a streamlined method;
- You name the computer with a standardized host name, to help with managing the machines;
- You install software the user needs on their machine;
- The new employee starts, and you streamline the setup process by providing instructions on how to use their new computer environment;
- Eventually, if a computer sees a hardware issue or failure, you investigate it;
  - If it's getting too old, you have to figure out where to recycle it and where to get new hardware;
- Finally, if a user leaves the company, you'll have to remove their access from IT resources and wipe the machine, so you can eventually reallocate it to someone else.

Imaging -- installing software and configuring settings on a new computer -- can get time-consuming. You'll have to learn automated ways to provision new machines so that you only spend minutes on this, and not hours.


### Routine Maintenance

When providing updates and maintenance for a fleet of machines, you don't want to immediately install updates as soon as they come in -- this would be way too time-consuming. 

Instead, to effectively update and manage hardware, you do what's called a **batch update**.
- A batch update is where, once every month or so, you update all your servers with the latest security patches.


### Vendors

Working with vendors or other businesses to buy hardware is commonly assigned to sysadmins.

Setting up business accounts with vendors like HP, Dell, Apple, etc is usually beneficial, since these companies can offer discounts to businesses.


### Troubleshooting and Managing Issues

Troubleshooting will take up most of your time as an IT support specialist.

Sysadmins have to troubleshoot issues at a larger scale.

Whatever the scenario, there are two critical skills for arriving at a good solution for your users:
1. Troubleshooting
  - Asking questions, isolating the problem, following the cookie crumbs, reading logs
2. Customer Service
  - Showing empathy, using the right tone of voice, dealing well with difficult situations


### In Case of Fire, Break Glass

To be prepared for anything, it's very important to make sure your company's data is routinely backed up somewhere. Preferably, far away from its current location.


## Applying Changes

### With Great Power Comes Great Responsibility

Avoid using administrator rights for tasks that don't require them.

Try to minimize the time spent in an administrative session.

Respect the privacy of others.
- Just because you can do something, doesn't mean you should do something.

Think before you type.
- Your actions can have much greater consequences as an administrator, compared to being a regular user.
- Writing out the steps you plan to take before doing them helps in two ways:
1. It allows you to plan ahead;
2. It serves as documentation.
- Documenting what you did is crucial when using administrator rights.
  - Recording the commands you executed lets you repeat the same process in the future and can fix problems that may arise later.

In Linux, the `script` command can record a group of commands as they are being issued along with their output.

In Windows PowerShell, there's an equivalent command called `Start-Transcript`

The recordMyDesktop tool can record the interaction with the graphical application.

With great power comes great responsibility
- The more you can do with your administrator rights, the more you can mess up.
- To minimize the impact of (inevitable) mistakes, make sure you can quickly revert your changes if something goes wrong.
- Make a copy of the state before changing it;
  - Keep your configuration in a version control system or by documenting what steps you need to go back to the previous state.

Reverting to the previous state is called a **rollback**.

Before you make a change, take a moment to think about what that would look like, and make sure you have copies of any information that could be lost.


### Never Test in Production

**Production** is the parts of the infrastructure where a certain service is executed and served to its users.

The **test environment** is usually a virtual machine running the same configuration as the production environment, but isn't actually serving any users of the service.

For an important service that must run during a configuration change, it's best to have a secondary or stand-by machine.

A **secondary** or **stand-by machine** will be exactly the same as a production machine, but won't receive any traffic from actual users until you enable it to do so.

For even bigger services, when you have lots of servers providing the service, you may want to have canaries.
- Canaries refer to a small group of servers to detect any potential issues in the larger changes you want to push out in the system.

Always use a test instance first, and only deploy the change to production after verifying that it works.


### Assessing Risk

The amount of time and effort to invest in changes depends on the risk involved.

We can assess the risk involved by considering how important the services to the infrastructure are, and how many users would be impacted if the service went down.

In general, the more users your service reaches, the more you'll want to ensure that changes aren't disruptive.

The more important your service is to your company's operations, the more you'll work to keep the service up.

You can also use these criteria to establish priorities for fixing a problem. If the problem is preventing people from doing their work, finding a solution to it should have a higher priority than solving a minor annoyance that can be worked around.


### Fixing Things the Right Way

- Before you start fixing a problem, make sure you can recreate the error, as you'll want to test your solution to make sure the problem is gone after you apply the fix.
- This is called a reproduction case.
  - A **reproduction case** is to create a roadmap to retrace the steps that led the user to an unexpected outcome.

When looking for a reproduction case, there are three questions you'll need to answer:
1. What steps did you take to get to this point?
2. What's the unexpected or bad result?
3. What's the expected result?

But remember: Always do this in your test instance, never in production.

Make sure you document all your steps and any findings.

After applying your fix, retrace the same steps that took you to the bad experience. If your fix worked, the expected experience should now take place.

