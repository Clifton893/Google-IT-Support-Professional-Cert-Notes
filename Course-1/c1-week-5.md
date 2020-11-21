# Week 5: Software


## Introduction to Software

*As an IT Support Specialist, you'll be in a position to not only know how a given piece of technology functions, but also how to help fix it when it breaks.*

- **Software** is how we, as users, directly interact with our computer.

- If *hardware* is the physical stuff that you can pick up and hold, *software* is the intangible instructions that tell the hardware what to do.


### What is Software?

#### Common software-related terms

- **Coding:** Translating one language to another.
  - Can be English to Spanish, or English to Morse Code, or English to binary.
  - When someone builds an application, we refer to it as *coding* an application.

- **Scripting:** Coding in a scripting language.
  - **Scripts** are mainly used to perform a single or limited-range task.

- **Programming:** Coding in a programming language.
  - **Programming languages** are special languages that software developers use to write instructions for computers to execute.

- The term *software* generally refers to something that was programmed.


### Types of Software

- **Copyright** is used when creating original work.

- **Open-source software (OSS)** is a type of software that can allow freedom of use, modification, and sharing.
  - A good example is the Linux kernel. 
  - LibreOffice, GIMP, and FireFox are other examples of OSS.

- Open-source projects are usually contributed to by developers who work on the project for free on their own time.
  - Some of the greatest software efforts were built by a community of volunteers.

- **Application software** is any software created to fulfill a specific need, like a text editor, web browser, or graphic editor.

- **System software** is software used to keep our core system running, like operating system tools and utilities.

- **Firmware** is software that's permanently stored on a computer component.
  - An example would be the BIOS.

- Sequential numbering trend is used when categorizing software versions.
  - Further reading: [Software versioning](https://en.wikipedia.org/wiki/Software_versioning)


### Revisiting Abstraction

*We can send binary code or bits to our CPU, then they'll use an instruction set to run those commands. But these CPUs might be from different manufacturers and may have different instructions.*

*[T]hanks to the efforts of computer scientists and the principle of abstraction, we can now use programming languages to write instructions that can be run on any hardware.*


### Recipe for Computing

- In the early days of computing, scientists needed to replace the tedious system of punchcards.
  - Eventually, they invented a new language: Assembly.

- **Assembly language** allowed computer scientists to use human readable instructions, assembled into code, that the machines could understand.
  - Assembly allowed computer scientists to provide instructions not in binary code, but in human-readable language.

- But during that time, a program written for a specific CPU could only be run on that CPU (or CPU family).
  - The need for a program that could run on many different types of CPUs led to the development of compiled programming languages.

- **Compiled programming languages** use human readable instructions, then send them through a compiler.
  - The compiler converts the human readable instructions and converts them into machine readable instructions.
  - This technique was invented by Admiral Grace Hopper in 1959 to make programming easier.

- Along the way, another language was invented that was interpreted, rather than compiled.
  - Interpreted languages aren't compiled ahead of time.
  - A file written in one of these languages is usually called a script.
 - *The script is run by an interpreter, which interprets the code into CPU instructions just in time to run them.*

*Along the way, another type of language emerged that was interpreted rather than compiled. Interpreted languages aren't compiled ahead of time. A file that has code written in one of these languages is usually called a Script. The script is run by an interpreter, which interprets the code into CPU instructions just in time to run them.*

#### What's the difference between compiled language and interpreted language?
*Interpreted languages are not broken into machine instructions beforehand, like compiled languages are.*

#### What's the benefit of scripting?
*As an IT support specialist, scripting can help you by harnessing the power of a computer to perform tasks on your behalf, allowing you to solve a problem once and then move on to the next thing.*


## Interacting with Software

### Managing Software

- Programs, software, and applications are synonymous with each other.

- There are different types of software, that perform specific functions.
  - *Drivers* which let us interact with our hardware.
  - *Applications* we use for our day-to-day job functions.
  - *Utilities* we use, such as calculators, settings, and other tools.

- You should always test new software before letting your company use it.

- Old software is another problem.
  - When you run old software on your machine, you expose yourself to cybersecurity attacks that take advantage of software bugs.
  - **Software bugs** are errors in software that causes unexpected results.

- Update your software constantly.

- **Software management** includes many tasks such as installing, updating, and removing software.
  - You want to make sure a worker's computer has all the software required for their job.


### Installing, Updating, and Removing Software on Windows

- **Git** is a version control system that helps keep track of changes made to files and directories.

- Remember to mirror the bit architecture of your CPU (32-bit or 64-bit) and mirror accordingly.

- **.exe** is a file extension found in Windows for an executable file.

- Sometimes after installing new software, your system prompts you to reboot. Make sure you do.
  - There might be system files or processes that also need to restart for your new software to work correctly.

- To verify you've installed a new program in Windows, navigate to `Add or remove programs` (or "Apps & features") 
  - From there, search in the text field in the "Apps & features" card.


### Installing, Updating, and Removing Software on Linux

- Unlike using the GUI shell to manage software in Windows, you use the CLI shell in Linux:
  - `apt install git`
    - `apt` is the command used in Ubuntu's package manager
    - `The `install` option will let you install something. 

- You need authorization to install on Linux, which requires the `sudo` command.
  - `sudo` stands for "superuser do," basically saying you are the administrator.

- To uninstall, run `sudo apt remove` followed by the program.


### Software Automation

It's easy to manage software on one machine; but what if you need to manage software across many machines?
- A solution to this is automation.

- **Automation** Makes processes work automatically.
  - Through automation, you can use programs and scripts to help with troubleshooting issues.
  - For example, reading hundreds of lines log files to discover an error, you can write a script to read the log for you; and print out only the relevant line.

---

## Questions for review

### Keywords

<details>
  <summary>What is software?</summary>
  <p>How we, as users, directly interact with a computer.</p>
</details>

<details>
  <summary>What is coding?</summary>
  <p>Translating one language to another.</p>
</details>

<details>
  <summary>What is a script?</summary>
  <p>Scripts are mainly used to perform a single or limited-range task.</p>
</details>

<details>
  <summary>What is a programming language?</summary>
  <p>A special language that software developers use to write instructions for computers to execute.</p>
</details>

<details>
  <summary>What is OSS?</summary>
  <p>Open-source software (OSS) is a type of software that can allow freedom of use, modification, and sharing.</p>
</details>

<details>
  <summary>What is firmware?</summary>
  <p>Firmware is software that's permanently stored on a computer component (like the BIOS).</p>
</details>

<details>
  <summary>What is a compiled programming language?</summary>
  <p>Human-readable instructions, sent through a compiler, which converts them into machine-readable instructions.</p>
</details>

~

<details>
  <summary>What is a driver?</summary>
  <p>Drivers are a type of software that let a computer interact with hardware.</p>
</details>

<details>
  <summary>What is an application?</summary>
  <p>Applications are software used for day-to-day functions.</p>
</details>

<details>
  <summary>What is a software bug?</summary>
  <p>Errors in software that cause unexpected results.</p>
</details>

### Concepts

<details>
  <summary>What's the difference between compiled language and interpreted language?</summary>
  <p></p>
</details>

<details>
  <summary>What's the benefit of scripting?</summary>
  <p></p>
</details>
