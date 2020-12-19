# Week 5: Process Management

## Life of a Process

### Programs vs Processes Revisited

Recall that **programs** are applications we can run (like Chrome); and that **processes** are programs that are running.

- When we launch a process, we're executing a program.
- When processes are run, they take up hardware resources like CPU and RAM

#### How processes work
- When you open up an application like a word processor, you're launching a process.
- That process gets assigned something called a **process ID** to uniquely identify it from other processes.
- The computer sees that the process needs hardware resources to run;
  - So the kernel makes decisions to figure out what resources to give it.

Besides visible processes, there are also **background processes**, also known as *daemon processes*.
- Background processes are processes that run in the background.
- We rarely see them, and rarely interact with them; but the system needs them to function.
  - They include processes like scheduling resources, logging, managing networks, and more.


### Windows: Process Creation and Termination

When Windows boots up, the first non-kernel user mode that starts is the Session Manager Subsystem, or `smss.exe`. This is the process in charge of setting the scene for the OS to work.
- It then kicks off the login process, called `winlogon.exe`
- It also starts the Client/Server Runtime Subsystem (`csrss.exe`), which handles running the Windows GUI and command line console.

Linux uses a process called `init`, but this is not equivalent to `smss.exe`.

In Windows, each new process created needs a parent to tell the operating system that a new process needs to be made. The child process inherits some things like variables and settings, which we collectively refer to as an **environment**.
- Unlike in Linux, Windows processes can operate independently of their parents.
- You can use a command prompt to stop processes via the `taskkill` utility.
  - A common way of using this utility is with an identification number, known as the **process ID (PID)** to tell task kill which process you'd like stopped.
  - Ex: `taskkill /pid PROCESSID


### Linux: Process Creation and Termination

- Linux processes have parent-child relationships.
  - This means that every process you launch comes from another command.
- Logically, if all processes come from another process, there must be an initial process that starts it all.
  - This is **init**
  - When you start up your computer, the kernel creates a process called `init`, which has a PID of `. 
  - `init` starts up other processes that we need to get our computer up and running.
- When processes complete their tasks, they'll generally terminate automatically.
- Once a process terminates, it will release all the resources it was using back to the kernel, so they can be used for another process.


## Managing Processes

### Windows: Reading Process Information

You can think of processes as programs in motion. There are different ways you can investigate which processes are running on a Windows computer, and more methods of interacting with them.

In Windows, the **Task Manager**, or `taskmgr.exe` is one way of obtaining process information. 
- You can open it with `Ctrl` + `Shift` + `Esc` key combination; or locate it through the Start Menu.
  - If you click on the processes tab, you can see a list of processes the current user is running; along with system-level processes the user can see.
  - The task manager tells you what app or image the process is running, along with the user who launched it, and the CPU or memory resources it's using.
- To kill a process, you can select any of the process rows and click the "End Task" button.

#### Obtaining Process ID
- While in task manager, you can click on the details menu option
  - Among the information displayed is the PID
- You can also see this information from both the command prompt and PowerShell:
  - In the command prompt, use the `tasklist` command to show all the running processes.
  - In PowerShell, you can use the cmdlet called `Get-Process` to do the same.


### Linux: Reading Process Information

To view the processes running on a Linux system, run the `ps -x` command. This shows you a snapshot of the current processes you have running.

From left to right:
- The PID is the process ID
- TTY is the terminal associated with the process
- STAT is the process status; 
  - An R here means the process is running, or waiting to run
  - A T is for stopped, meaning a process has been suspended
  - S is for interruptible sleep, meaning the task is waiting for an event to complete before it resumes
- TIME is the total CPU time the process has taken up
- And CMD is the name of the command that we're running

Another way to view process information is to view their corresponding files, in the `/proc` directory.
The `/proc` directory is not very practical when you need to troubleshoot issues with processes.


### Windows: Signals

- To tell a process to quit at the system level, we use something called a signal. 
- A **signal** is a way to tell a process that something's just happened.
- You can generate a signal with special characters on your keyboard, and through other processes and software.
  - One of the most common signals you'll come across is SIGINT, which stands for "signal interrupt"
  - You can send this signal to a running process with the `CTRL` + `C` key combination.


### Linux: Signals

Much like in Windows, the signal interrupt (SIGINT) process can be run by `CTRL` + `C`


### Windows: Managing Processes

**Process Explorer** is a utility Microsoft created to let IT support specialists, system administrators, and other users look at running processes.
- It doesn't come with Windows, and you need to download it from Microsoft's website.
- Process Explorer presents a view of the current/active processes in the top window pane.
  - You can also see a list of files a selected process is using in the bottom window pane.
  - **MUI** stands for **multilingual user interface**, and contains a package of features to support different languages.
- A nested process indicates that it's a child process.
- Right-click will present several options, including Kill Process, Kill Process Tree, Restart, or Suspend.
- If you restart a process using the Process Explorer utility, the new parent of that process will be Process Explorer itself (since it launched it)

In summary, the Task Manager, the command prompt's tasklist utility, and the `Get-Process` commndlet from PowerShell all help you gather information about processes running on Windows OS.


### Linux: Managing Processes

#### SIGTERM
- We can terminate a process using the `kill` command
  - A `kill` command without any flags sends a termination signal, or SIGTERM
  - This will kill the process; but gives it some time to clean up the resources it was using
  - If you don't give the process a chance to clean up, it could cause file corruption

#### SIGKILL
- This signal does its very best to make sure your process absolutely gets terminated, without giving it time to clean up
- To send a SIGKILL signal, you add a flag to the kill command: `kill -KILL [process]`
- This should be a last resort for process termination
  - Since it doesn't do any cleanup, you could do more harm than good to your files

#### SIGTSTOP
- If you want to pause a process instead of terminating it, you can do this with the SIGTSTP signal
  - This means "terminal stop," which puts your process in a suspended state
- Run `kill -TSTP` to achieve this
  - The keyboard combination `Ctrl` + `Z` also achieves this
- To resume the execution of the process, the **SIGCONT** ("continue signal") can be run:
  - `kill -CONT`


### Mobile App Management

[ Take notes ]

Rather than view the list of running processes, mobile operating systems (like iOS and Android) let you manage mobile apps that are running on the OS.

- Both iOS and Android let you open the App Switcher, where you see a list of apps running on the OS.
- The app you're using is called the *foreground app*
- The other apps are called *background apps*
- Background apps are suspended -- paused, but not closed
- The App Switcher enables you to swipe up to close background apps


## Process Utilization

### Windows: Resource Monitoring

In Windows, one of the most common ways to take a peek at how the system resources are doing, is by using the **Resource Monitoring** tool. You can run it from the Start menu.

Another method is to use PowerShell, specifically `Get-Process`. Sorting and selecting a search through `Get-Process` is a helpful way to filter down to just the data you need.


### Linux: Resource Monitoring

#### top
- A useful command to find out what your system utilization looks like in real time, is the `top` command.
- `top` shows us the top processes that are using the most resources on our machine.
  - We can also get a quick snapshot of total tasks running or idle, CPU usage, memory usage, and more.
  - "Percentage CPU" and "percentage mem" show what CPU and memory usage a single task is taking up
- To exit the top command mode, hit the `Q` key ("quit")
- If you find that top shows a certain task is taking up a lot of memory or CPU, you can investigate what the process is doing (terminating if necessary)

#### uptime
- Another useful tool for resource utilization is the `uptime` command
- This command shows information about the current time, how long your system's been running, how many users are logged on, and what the load average of your machine is
  - Load averages are useful when you need to see how your machine is doing over a certain period of time
  - In uptime, you can show the average CPU load in 1, 5, and 15-minute intervals

#### lsof
- The `lsof` command lists open files and what processes are using them.
- This command is useful for tracking down processes that are holding open files
