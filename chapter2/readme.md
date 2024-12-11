# Questions and Answers:

1. what is shell?
- A shell is a program that runs commands
- The shell also serves as a small programming environment
-  There are many different Unix shells, but all derive  features from the Bourne shell (/bin/sh)
-  Linux uses an enhanced version of the Bourne shell called bash or the “Bourne-again” shell.
- to change the default shell use `chsh` command

2. what is streams?
	- Unix processes use I/O streams to read and write data. Processes read data from input streams and write data to output streams.
	- The reason cat adopts an interactive behavior when you doesn't give an input file to it has to do with streams. When you don’t specify an input filename, cat reads from the standard input stream provided by the Linux kernel rather than a stream connected to a file. In this case, the standard input is connected to the terminal where you run cat
	- The kernel gives each process a standard input stream from where it can read its input.
	- The kernel gives each process a standard output stream where it can write its output.
	- There is a third standard I/O stream, called standard error.

3. what happened if The shell doesn't find anything to expand?
	```bash
	ls *.xyz
	```

	- If no `.xyz` files exist, the shell may leave `*.xyz` as is (depending on the shell settings) and pass it directly to the `ls` command. The `ls` command would then treat it as a literal string, not as a wildcard.

4. How to disables expansion?
	- Quoting disables expansion:
	```bash
	echo '*'
	```

<div style="page-break-after: always;"></div>


5. what are special charaters?
    <p align='center'>
    <img width="75%" src="./Img/Special Characters.jpeg"/>
    </p>


6. what dose sort command do?
	- The sort command quickly puts the lines of a text file in alphanumeric order

7. what are online manual section ?
    <p align='center'>
    <img width="75%" src="./Img/Online Manual Sections.jpeg"/>
    </p>

8. ps Command Options?
	```bash
	ps x # Show all of your running processes. 
	ps ax # Show all processes on the system, not just the ones you own. 
	ps u # Include more detailed information on processes. 
	ps w # Show full command names, not just what fits on one line.
	```


9. Process Termination
```bash 
kill pid  # to terminate a process
kill -STOP pid  # to stop a process 
kill -CONT pid  # to continue a process
```

<div style="page-break-after: always;"></div>



10. what are job control?
	- you can send a TSTP Using CTRL-C to terminate a process that is running in the current terminal is the same as using kill to end the process with the INT (interrupt) signal. The kernel gives most processes a chance to clean up after themselves (with signal handler mechanism).
	- you can send a TSTP signal with CTRL-Z to stop the current process and then start the process again by entering fg (bring to foreground) or bg (move to background)

11. what are Background Processes?
	- Normally, when you run a Unix command from the shell, you don’t get the shell prompt back until the program finishes executing. However, you can detach a process from the shell and put it in the “background” with the ampersand (&); this gives you the prompt back.

	<p align='center'>
    <img width="75%" src="./Img/using&.jpeg"/>
    </p>

12. what is nohub command?
	- If you’re remotely accessing a machine and want to keep a program running when you log out, you may need to use the nohup command

13. to list all groups you are in
	- use the groups command 

14. what are sympolic links?
	- A symbolic link is a file that points to another file or a directory, effectively creating an alias (like a shortcut in Windows).

15. display file permissions 
    <p align='center'>
    <img width="75%" src="./Img/The pieces of a file mode.jpeg"/>
    </p>

16. How to change permissions?
```bash
chmod g+r file  # add read permission to group
chmod u+r file  # add read permission to user 
chmod o+r file  # add read permission to other
chmod u+w file  # add write permission to user
chmod u+x file  # add execute permission to user
```

<div style="page-break-after: always;"></div>



17. change permissions using binary representations?

    <p align='center'>
    <img width="75%" src="./Img/Absolute Permission Modes.jpeg"/>
    </p>


18. to compress one file (can't compress directories):
```bash
gzip file # to compress a file
gunzip file.gz # to unzip a file 
```

19. to compress directories and files?
```bash 
tar cvf archive.tar file1 file2 directory/  # to compress a directory and 2 files

# `c`: _Create_ a new archive.
# `v`: _Verbose_ output, showing files as they are added to the archive.
# `f`: Specifies the name of the archive file (in this case, `archive.tar`).
```

```bash
tar cv test test2 projects/
```

In this case, the system would assume you're writing to or reading from a tape drive, which is not typically desired on modern systems.

By always using `f`, you clearly specify the destination file or input source for the archive operation.


<div style="page-break-after: always;"></div>




## System Hierarchy:

- /bin Contains ready-to-run programs (also known as executables), including most of the basic Unix commands such as ls and cp

- /dev Contains device files.

- /etc This core system configuration directory (pronounced EHT-see) contains the user password, boot configrations, device, networking, and other setup f iles.

- /home Holds home (personal) directories for regular users. Most Unix installations conform to this standard.

- /lib An abbreviation for library, this directory holds library files con taining code that executables can use. There are two types of libraries: static and shared. The /lib directory should contain only shared librar ies, but other lib directories, such as /usr/lib, contain both varieties as well as other auxiliary files.

- /proc Provides system statistics through a browsable directory-and-file interface. The /proc directory contains information about currently running processes as well as some kernel parameters

- /run Contains runtime data specific to the system, including certain process IDs, socket files, status records, and, in many cases, system log ging

- /sys This directory is similar to /proc in that it provides a device and system interface.

- /sbin The place for system executables. Programs in /sbin directories relate to system management.

- /tmp A storage area for smaller, temporary files that you don’t care much about. Any user may read to and write from /tmp. Many programs use this directory as a workspace. don’t put it in /tmp because most distributions clear /tmp when the machine boots and some even remove its old files periodi cally.

- /usr Although pronounced “user,” this subdirectory has no user files. Instead, it contains a large directory hierarchy, including the bulk of the Linux system. Many of the directory names in /usr are the same as those in the root directory (it was to keep space requirements low for the root.) 

- /var The variable subdirectory, where programs record information that can change over the course of time. System logging, user tracking, caches, and other files that system programs create and manage are here. 

- /boot Contains kernel boot loader files. These files pertain only to the very first stage of the Linux startup procedure,
- /media A base attachment point for removable media such as flash drives that is found in many distributions.
- /opt This may contain additional third-party software

<div style="page-break-after: always;"></div>




## The /usr Directory:
### contains the following:
- /include Holds header files used by the C compiler.
- /local Is where administrators can install their own software. Its struc ture should look like that of / and /usr. 
- /man Contains manual pages. 
- /share Contains files that should work on other kinds of Unix machines with no loss of functionality. These are usually auxiliary data files that programs and libraries read as necessary
---
## Kernel Location:
On Linux systems, the kernel is normally a binary file /vmlinuz or /boot/ vmlinuz. A boot loader loads this file into memory and sets it in motion when the system boots.

Once the boot loader starts the kernel, the main kernel file is no longer used by the running system. However, you’ll find many modules that the kernel loads and unloads on demand during the course of normal system operation. Called loadable kernel modules, they are located under /lib/modules.

---
## Running Commands as the Superuse:
### disadvantages:
• You have no record of system-altering commands. 
• You have no record of the users who performed system-altering commands.
• You don’t have access to your normal shell environment.
• You have to enter the root password (if you have one).

<div style="page-break-after: always;"></div>




## NOTES:
- Pressing CTRL-D on an empty line stops the current standard input entry from the terminal with an EOF (end-of-file) message (and often terminates a program). Don’t confuse this with CTRL-C, which usually terminates a program regardless of its input or output.
- the bash shell reads the PS1 variable before displaying the prompt.
- Don’t put any spaces around the = when assigning a variable
- manual pages
```bash
man 5 passwd #display the /etc/passwd file description
man passwd # equal to man 1 passwd --> display the passwd command info 

```

- you can enter set -C to avoid clobbering in bash.) if you use this command you are forbidden to override an existing file
```bash
set -C # to undo use set +C
```

- No such file or directory is known as ENOENT “Error NO Entity.”
- PIDs are unique for each process running on a system. However, after a process terminates, the kernel can eventually reuse the PID for a new process.


- $\$ is a shell variable that evaluates to the current shell’s PID.

```bash
echo $$ # to print the process id of the current shell  
```

 - Each read, write, and execute permission slot is sometimes called a permission bit because the underlying representation in the operating system is a series of bits. Therefore, you may hear people refer to parts of the permissions as “the read bits.”
- `sudo` (short for **superuser do**)

<div style="page-break-after: always;"></div>



- to display all commands that you runs as sudo 

```bash
journalctl SYSLOG_IDENTIFIER=sudo
```

- to edit etc/passwd
```bash
sudo vipw
```

- to edit /etc/sudoers
```bash
sudo visudo #This command checks for file syntax errors after you save the file
```

```bash
cat /var/log/auth.log #print log commands
```