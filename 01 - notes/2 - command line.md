# Command Line Essentials
---

## 1. Introduction to the Command Line

The **Command Line Interface (CLI)** is a text-based way to interact with Linux.
Instead of clicking buttons, you type commands that directly control the system.

Why the command line matters:
- Full control over the system
- Faster and more efficient than graphical tools
- Essential for remote server and cloud administration

⚠ **Important**
Linux commands are concise but powerful.
A small change in a command can produce very different results.
Always double-check commands—especially those that modify or delete files.

---

## 2. Launching the Terminal and Bash

### Launching the Terminal (Ubuntu)
- Open the **Applications** menu
- Search for **Terminal**
- Launch it

### Confirming Bash as Your Shell
Most Linux systems use **Bash** by default.

Check your Bash version:
```bash
echo "${BASH_VERSION}"
```
If no version is displayed, start Bash manually:
```
bash
```
(Optional) Set Bash as the default shell:
Terminal Preferences → Command → Run command as login shell

## 3. Structure of a Bash Command
Most Bash commands follow this structure:
```
command [options] [arguments]
```
Example: echo <br>
Print simple text:
```
echo 'Bash is amazing!'
```
Disable the newline (-n) and enable escape characters (-e):
```
echo -ne 'Bash\tis\namazing!'
```
Multiple options can be combined:
```
echo -en 'text'
```
## 4. Navigating the File System

Linux file systems differ from Windows:

- No drive letters (C:, D:)
- The root directory (/) is the starting point
- Each user has a home directory:<br>

Key Commands
- Print current working directory:
```
pwd
```
- List files/directories:
```
ls              # list current directory
ls -a           # include hidden files       
ls -l           # detailed list with permissions and timestamps       
ls /path/to/dir # list contents of specific directory
```
- Change directory:
```
cd folder             # go into folder     
cd ..                 # move up one directory    
cd ~ or cd            # go to home directory    
cd /absolute/path     # go to absolute path
```

## Absolute vs. Relative Paths
- **Absolute Paths**  (
/home/user/Desktop 
): Complete path starting from root (/).
- **Relative Paths**  (
../Desktop 
): Path relative to current directory.
----

## 5. Getting Help on Commands
Use built-in help options to find command details:

- Quick Help: 
```
command --help
command -h
```
Example: 
```
ls --help 
```
- Detailed manual pages (*man* pages):
```
man ls
```
if man not installed run this command in your terminal :
```
sudo apt install man-db manpages-posix manpages-dev manpages-posix-dev
```
then:
```
sudo mandb
```

otherwise: 
Online resources (e.g., Stack Overflow, Linux forums or ChatGPT) are also valuable for additional help.
---

## 6. Creating Files and Directories

