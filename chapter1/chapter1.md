# Questions and Answers:

1. What is the differences between os and kernel ?
	- The kernel is the core part of the OS. It directly interacts with the hardware and provides low-level services, like memory management, process scheduling, and hardware communication.
	- os includes kernel and application

	<p align='center'>
	<img width="75%" src="Img/General Linux system organization.jpeg"/>
	</p>

<br>

2. what is kernel?
	- kernel, which is the core of the operating system. The kernel is software residing in memory that tells the CPU where to look for its next task. Acting as a mediator, the kernel manages the hardware (especially main memory) and is the primary interface between the hard ware and any running program


<br>


3. what is process?
	- Processes—the running programs that the kernel manages --> Processes are programs that are running, and the kernel manages them. These processes together form the top part of the system, called **user space**. A more specific name for a process is a **user process**, even if it doesn’t involve direct user interaction. For example, web servers also run as user processes.




<div style="page-break-after: always;"></div>




4. user space vs kernel space?
	- User space refers to the parts of main memory that the user processes can access. If a process makes a mistake and crashes, the consequences are limited and can be cleaned up by the kernel.
	- The memory area that only the kernel can access is called kernel space.
	
	| **Aspect**             | **User Mode**                            | **Kernel Mode**                         |
	| ---------------------- | ---------------------------------------- | --------------------------------------- |
	| **Privilege Level**    | Lower privilege                          | Highest privilege                       |
	| **Access to Hardware** | Limited access; cannot interact directly | Full access to hardware and peripherals |
	| **Crash Impact**       | Only the application crashes             | System-wide crash if something fails    |
	| **Execution**          | Runs in user space                       | Runs in kernel space                    |
	| **Performance**        | Slower, due to restricted access         | Faster for hardware-related operations  |
	| **Examples**           | Applications, User programs              | Device drivers, Operating System kernel |
	| **Switching Overhead** | Requires system calls (higher overhead)  | Direct execution, no system call needed |


<br>

5. can a user process completely wreck the data on a disk?
	- With the correct permissions, yes—and you might consider this to be fairly dangerous. There are safeguards to prevent this, however, and most processes simply aren’t allowed to damage the system in this manner.

<br>

6. what is a state?
	- a state is a particular arrangement of bits For example, if you have four bits in your memory, 0110, 0001, and 1011 represent three different states.
	- You’ll often hear the term state when talking  about memory, processes, the kernel, and other parts of a computer system. Strictly speaking

<br>

7. do we use something rather than state ?
	- Instead of describing a state using bits, you describe what something has done or is doing at the moment. For example, you might say, “The process is waiting for input” or, “The process is performing Stage 2 of its startup.
	- Because it’s common to refer to the state in abstract terms rather than to the actual bits, the term image refers to a particular physical arrangement of bits

<div style="page-break-after: always;"></div>



8. What is the kenel's Job (in brief)?
	- Nearly everything that the kernel does revolves around main memory. One of the kernel’s tasks is to split memory into many subdivisions
	- Each process gets its own share of memory, and the kernel must ensure that each process keeps to its share
	The kernel is in charge of managing tasks in four general system areas:
	    - Processes The kernel is responsible for determining which processes are allowed to use the CPU. 
	    - Memory The kernel needs to keep track of all memory—what is currently allocated to a particular process, what might be shared between processes, and what is free. 
	    - Device drivers The kernel acts as an interface between hardware (such as a disk) and processes. It’s usually the kernel’s job to operate the hardware.
    	- System calls and support Processes normally use system calls to communicate with the kernel



<br>



9. How context switching work ?
	1. The CPU (the actual hardware) interrupts the current process based on an internal timer, switches into kernel mode, and hands control back to the kernel. 
	2. The kernel records the current state of the CPU and memory, which will be essential to resuming the process that was just interrupted. 
	3. The kernel performs any tasks that might have come up during the preceding time slice (such as collecting data from input and output, or I/O, operations). 
	4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready to run and chooses one. 
	5. The kernel prepares the memory for this new process and then pre pares the CPU. 
	6. The kernel tells the CPU how long the time slice for the new process will last. 
	7. The kernel switches the CPU into user mode and hands control of the CPU to the process

<br>

10. When dose the kernel work?
	- The context switch answers the important question of when the kernel runs. The answer is that it runs between process time slices during a context switch

<br>

11. memory management 
    - The kernel must manage memory during a context switch, which can be a complex job. The following conditions must hold: 
	    -  The kernel must have its own private area in memory that user processes can’t access. 
	    - Each user process needs its own section of memory. 
	    - One user process may not access the private memory of another process.
	    -  User processes can share memory. 
	    - Some memory in user processes can be read-only. 
	    - The system can use more memory than is physically present by using disk space as auxiliary

<br>

12. what are system calls?
    - There are several other kinds of `kernel features available to user processes. For example, system calls (or syscalls) perform specific tasks that a user process alone cannot do well or at all

<br>


13. fork() vs exec()
	Two system calls, fork() and exec(), are important to understanding how processes start: fork() When a process calls 
	- fork(), the kernel creates a nearly identical copy of the process. 
	- exec() When a process calls exec(program), the kernel loads and starts program, replacing the current process.


<br>



14. what happened when you type ls?
	- When you enter ls into a terminal window, the shell that’s running inside the terminal window calls fork() to create a copy of the shell, and then the new copy of the shell calls exec(ls) to run ls.
	<p align='center'>
	<img width="75%" src="Img/Starting a new process.jpeg"/>
	</p>

	- This design provides isolation and stability. If the `ls` command crashes or misbehaves, it doesn’t affect the shell or other parts of the system.


<br>


15. what is a user?
	- The Linux kernel supports the traditional concept of a Unix user. A user is an entity that can run processes and own files.
	- the kernel does not manage the usernames; instead, it identifies users by - simple numeric identifiers called user IDs
	- Every user-space process has a user owner
	- A user may terminate or modify the behavior of its own processes but it cannot interfere with other users’ processes.
	- users may own files and choose whether to share them with other users.


<div style="page-break-after: always;"></div>



<br>

16. How user space work?
	- Because a process is simply a state (or image) in memory, user space also refers to the memory for the entire collection of running processes. (You may also hear the more informal term userland used for user space; sometimes this also means the programs running in user space.)

	- Most of the real action on a Linux system happens in user space. Though all processes are essentially equal from the kernel’s point of view, they perform different tasks for users.

	- The bottom level tends to consist of small components that perform single, uncomplicated tasks. The middle level has larger components such as mail, print, and database services. Finally, components at the top level per form complicated tasks that the user often controls directly. Components also use other components. Generally, if one component wants to use another, the second component is either at the same service level or below.



	<p align='center'>
	<img width="75%" src="Img/Process types and interactions.jpeg"/>
	</p>



<br>




17. what is the root user?
	-  the most important user to know about is root 
	- root may terminate and alter another user’s processes and access any file on the local system
	- root is known as the superuser
	- A person who can operate as root—that is, who has root access—is an administrator on a traditional Unix system


<br>

18. what is groups?
	- Groups are sets of users. The primary purpose of groups is to allow a user to share file access to other members of a group


<div style="page-break-after: always;"></div>

<br>


### NOTES:
- The Linux kernel can run kernel threads, which look much like processes but have access to kernel space. Some examples are kthreadd and kblockd
- A CPU is just an operator on memory; it reads its instructions and data from the memory and writes data back out to the memory.
- The kernel is responsible for context switching
- each process uses the CPU for a small fraction of a second, then pauses; then another process uses the CPU for another small fraction of a second;
- The act of one proscess giving up control of the CPU to another process is called a context switch.
- Each piece of time—called a time slice
- The implementation of a memory address map is called a page table.
- all new user processes on a Linux system start as a result of fork()
- you run exec() to start a new program instead of running a copy of an existing process.
- Operating as root can be dangerous. It can be difficult to identify and correct mis takes because the system will let you do anything,
- as powerful as the root user is, it still runs in the operating system’s user mode, not kernel mode.
- The root user still operates in **user mode**, but the kernel interprets root's actions as having the authority to request any system operation. While the root user can't directly access hardware or switch to kernel mode, its requests to the kernel are almost never denied, giving it immense power.
- Only the kernel and trusted kernel-level code (like device drivers) operate in kernel mode.
