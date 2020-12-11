# Week 1: Navigating the System

## Basic Commands

- The command line interpreter in **Linux** is called a **shell**, and the language that we'll use to interact with this shell is called **Bash**.

#### Directories

- The **file system** controls how data is stored and retrieved in a computer.
- Files and folders are organized in a hierarchical directory tree.
- A main directory branches off and holds other directories and files.
  - We call the location of these files and directories **paths**.

#### PowerShell Commands
A **wildcard** is a character that's used to help select files based on a certain pattern.
  - The asterisk `*` represents the wildcard

- The `-recurse` parameter lists the content of the directory
  - If there are any subdirectories in that listing, it will recurse (or repeat) the directory listing process for each of those subdirectories.
- `-verbose` will output one line for each file of the directory being copied.
  - Unlike in Bash, these flags go after the destination in PowerShell

- The command to remove files and directories is `rm` (remove). 
  - You can append with the `-force` parameter, to remove protected or important files.

To delete a folder and its contents, remember to append with the recurse parameter.
  - Ex: `rm ~ /misc_folder -Recurse`


### Windows

The main directory in a Windows file system is called the **C Drive**

- In Windows, subdirectories are backslashes `\`, unlike Linux, which uses forward slashes `/`
- An **alias** is a nickname for a command
  - **parameters** tag onto a command, to specify additional options

- An **absolute path** is one that starts from the *main directory*; a **relative path** is the path from your *current directory*.



### Linux

The main directory in a Linux file system is called the **root directory** (`/`)

- All files and folders in a Linux system are part of a bigger tree-like structure, rooted at `/` (aptly called *root*)
- All file names are case sensitive


- Similar to Windows command parameters, a **flag** is a way to specify additional options for a command.
  - An example is the `--help` flag, which shows useful information on how to use a command.

#### Appending commands
- `ls -la` is the same thing as `ls -l -a`, and both work the exact same way.
- However, the order of the flag determines which order it goes in.

#### Bash Commands
- `-r` is the flag for recursive copy
- To delete a folder and its contents, remember to use the recurse parameter.
  - Ex: `rm -r misc_folder`


## File and Text Manipulation

Notepad++ can search for file content across directories (`ctrl` + `shift` + `f`)

#### PowerShell

`-Head` and `-Tail` are useful for viewing the first (or last) lines in a file.

To figure out the difference between PowerShell commands and aliases, use the command `Get-Alias x` (where x is the command you're determining)
- PowerShell commands are long and descriptive, which do help explain; but they require extra typing.

There are three ways you can run commands in Windows:
1. PowerShell commands
2. Alias name (Bash command)
3. cmd.exe 
  - `/?` serves as get-help for cmd.exe (ex: `dir /?`)

`Select-String` is a powerful tool when combined with wildcards

- The `-Filter` parameter will filter the results for file names that match a pattern.
  - Ex: `ls 'C:\Program Files\' -Recurse -Filter *.exe`

In PowerShell, `echo` is an alias for `Write-Output`


#### Bash

- `less` is used for viewing large files in the terminal
  - You can navigate with up and down; page up/down; `g` moves to the beginning of a text file; `G` moves to the end of a text file; 
  - `/word_search` allows you to search for a word or phrase
  - `q` allows you to quit less and return to the shell
 - `head` and `tail` operate as they do in PowerShell

In Bash, you can search for words within files that match a certain pattern using the `grep` command.


### I/O Streams

#### Windows

Each process in Windows has three different streams:
- Standard in / `stdin`
- Standard out / `stdout`
- Standard error `stderr`

The CLI input you provide through the keyboard goes to the `stdin` stream; the process then communicates back to you by putting data into the `stdout` stream, which the CLI prints onto your screen.

The `>` is the **redirector operator**, which lets us change where we want our standard output to go.
  - Instead of sending it to your screen, you can send it to a file.

The `>>` is another redirector operator, which can append information to an existing file (rather than overwrite it).

The `|` is the **pipe operator**, which can send the output of one command to the input of another command.
  - An example would be searching for a string in wildcard files, then extracting that string to a new file.
  - Ex: `cat words.txt | Select-String st > st_words.txt

You can redirect standard error to **$null**, which is like a black hole.



#### Linux

Linux uses the same I/O streams of `stdin`, `stdout`, and `stderr`

The **standard in redirector operator** is `<` (less-than sign), and gets input from a file, not from the keyboard.
  - Ex: `cat < file_input.txt`

The **standard error redirector operator** is `2>`, used to redirect the error messages of some output.

`/dev/null` serves as the $null variable for Linux


**Regular expressions** are used to help you do advanced pattern-based selection.

### Create, Modify, and Remove Files/Folders in Linux

#### Creating directories
- Directories (folders) in Linux are created using the `mkdir` command. 
- The command takes the directory name as the argument
  - Ex: `mkdir dir_name`
- Multiple directories can be supplied as arguments, and mkdir will create all of them:
  - Ex: `mkdir dir1 dir2 dir3`
- mkdir can take three options:
1. `-p` allows mkdir to create parent directories if they don't exist
2. `-m` (mode) used to set permissions of directories during creation
3. `-v` run command in verbose mode

#### Removing empty directories
- To remove empty directories, use the `rmdir` command.
  - The name of the directory being removed is passed as an argument
    - Ex: `rmdir dir_name`
- Like creation, multiple directories can be passed as arguments.
  - Ex: `rmdir dir1 dir2 dir3`
- rmdir only takes one option:
  - `-p` remove parent directories, but only if they're also empty

#### Creating files
- The touch command is used to change the modification and access times of a file.
- If the file doesn't exist, the command is used to create a file with default permissions.
  - Ex: `touch empty_file`
- `-c` do not create file if it doesn't exist

### Copying, moving, and deleting files and directories

- You can use a "dot" to copy or move files to the current directory.
  - Ex: `user@pc /home/user/Pictures $ mv /home/user/Images/Vacation.jpg .`

#### Searching in files
- **grep** is a super-powerful Linux command used to search through files for strings. 
- grep has many options and flags:
  - `-r` search recursively
  - `-w` match the whole word
  - `-n` only in line number
  - `-e` match pattern
  - `--include` and `--exclude` files in the search
  - `--include-dir` and `--exclude-dir` directories in the search
- Ex: `grep -rw /home/user/Downloads -e "vacation"`
