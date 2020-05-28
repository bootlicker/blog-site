---
title: "What is an Operating System?"
date: 2019-12-27T05:55:45+08:00
draft: false
---

# THE MINIX BOOK: GET IT UP YA! (Chapter One)
 
 -- BOOK SYNOPSIS and BASIC CONCEPTS --
 
There are several major core components of an operating system:

  * Processes
  * Files
  * Memory
  * I/O

The book is divided up into major chapters which deal exhaustively
with each topic, but for the purposes of this synopsis, we will deal
with these four topics briefly under the headings:

  * Processes
  * Files
  * The Shell
  * System Calls
  
## What is an Operating System?

Tanenbaum recommends defining an operating system both:

  1. An "Extended Machine"; and
  2. A Resource Manager.
  
The best elucidation of what is meant by these two terms comes from
the summary of the chapter, because much of these introductory
paragraphs are just platitudes that list the components of a computer,
and don't actually explain anything.

From the summary:

With respect to the "resource manager" attribute or aspect of the
definition of an operating system, this means that "the operating
system needs to efficiently manage the resources of the system".

Regarding the "extended machine" view, Tenanbaum says: "The job of the
operating system is to provide its users with a virtual machine that
is more convenient to use than the actual bare metal of the computer".

## Processes

A program in execution within an operating system is defined as a
"process".

Tenanbaum: "Associated with each process is its **address space**, a
list of memory locations from some minimum to some maximum, to which the
process is permitted to read and write."

The address space contains the **executable program**, the **program's data**,
and its **stack**. Associated with the program is some set of CPU
registers, including the **Program Counter** (PC), **Stack Pointer**
(SP), &c.

### Multiprogramming

One important key concept of the Process Management aspect of
operating systems is "multiprogramming". This means most often
systematically, and at other times and arbitrarily and reactively
being able to start, stop, suspend and kill processes at will.

#### Suspending processes

When a process is suspended, it has to be started in exactly the same
state as it was stopped. All the information abut the state of that
process has to be recorded down, somewhere, somehow.

In many operating systems, all the information about the process,
other than the contents of its own address space, is stored in an
operating system table called the **process table**, which is an array
(or linked list) of structures, one for each process currently in
existence.

Therefore, a suspended process consists of its address space, usually
called its "core image", alongside its "process table entry", which
contants the state and name of its associated CPU registers.

### Process Management System Calls

Commands or requests sent to the operating system to manipulate or
read information about processes, whether they be from a process about
itself or another one, is called "process management", and the request
or instruction sent to the operating system is called a "system call".

Even Graphical User Interfaces can manage operating system
processes. GUIs are just very simple command interpreters. And of
course command line shells or terminal emulators are obviously able to
manipulate operating system process management by issuing system
calls.

### Interprocess Communication

  * Processes can create other processes. Processes that are created
    from others are called 'child' processes, and the ones that create
    them are called 'parent' processes.
  * Related processes that are cooperating to get some job done often
    need to communicate with one-another and synchronise their
    activities. This set of interrelationships is called
    **interprocess communication**
  * Processes *themselves* are able to make system calls. The system
    calls that *processes* are commonly known to make are:
      * Request more memory
	  * Release unused memory
	  * Wait for a child process to terminate
	  * "Overlay its own program with another, different one".
	  
### Signals

Sometimes we need to convey information to a process that is not
waiting or expecting this information. Here's an example:

> A process is sending some information to another host somewhere
> outside this operating system. The process will request the
> operating system to notify it of the exhaustion of a time limit by
> setting a timer, so that the process can determine whether to
> retransmit the information.

This is called an 'alarm' signal. Signals are special instructions
that operating systems send to processes to interrupt their normal and
autonomous operation. This is a really important and powerful feature
of operating systems. Signals are the software equivalent or analogue
of hardware interrupts. They are instrumental in being able to
negotiate multiprogramming operating system environments.

When a process receives a signal, the process stops what it is doing,
saves its state to memory, and goes into a special signal handling
procedure. When that is done, the process recovers its old state, and
goes back to what it was doing.

There are many and various types of signals, and reasons for using
them. (Like the KILL signal that we're all familiar with >:3). Some
interesting signals are ones generated and sent due to traps in the
kernel detected by hardware, like illegal instructions or invalid
addresses.

I am going to skip over the text on UIDs, GIDs, because everyone I am
addressing this to has some conception of UNIX PIDs which is of a good
working standard.

## Files

### Definiton of Some Terms

A "file pathname" is the location of a file relative to the location
of the root of the filesystem. File systems in this book are assumed
to be hierarchical. So, we all know /home/USERNAME/... etc, or
/dev/sda... etc.

Every process has a "working directory", which is the files in a path
relative to this defined path that the process "looks for".

"File permissions" -> self explanatory, already prior knowledge of
most UNIX-like operating system users. Turns out they're a part of how
the operating system manages system calls, processes, and memory!! Who
knew??

"Mounting file systems" -> attaching different directory hierarchies,
sometimes with different filesystem architectures, to some location
relative to the root of *some other* file system hierarchy.

### General Concept of 'Files' in Operating Systems

Operating systems provide programmers and users with abstractions of
the I/O and disk hardware. That way, the arbitariness and pecularity
of the hardware, and the file system digital structure, is hidden, but
still able to be manipulated just as effectively, if not more
powerfully.

### Files, File Systems, and System Calls

System calls, much like in process management, are used to manipulate
files and file systems. System calls can:

  * Create files
  * Remove files
  * Read from files
  * Write to files
  
A lot of these operations are dependent on another concept called
'opening' and 'closing' files. This is fairly intuitive. A file that
hasn't been opened cannot be written to, and a file that has not been
closed has not entered a state in which it is ready to be read by
other processes.

It goes without saying that, yep, you guessed it, system calls all
deal with manipulating *directories* of files as well as just the
files.

A final note: both processes and file systems are organised
hierarchically, but the similarity stops there. Processes usually only
exist temporarily, and for matters of minutes, but files have been
known to exist in wild for many multiples of years.

#### Special Files

These objects in file systems are provided in order for devices, and
other kinds of complex hardware components to look like files. This
special kind of object allows the use of identical system calls for
access and manipulation of the hardware.

#### Special Files in MINIX 3

In MINIX 3, there are two kinds of special files, and as far as I can
tell, people who are UNIX-like users will already be very familiar
with them:

  * Block Files
  * Character Files
  
The first treat randomly accessible hardware components, such as hard
disks or CD-ROMs &c, as files in the file system. The great power of
this form of hardware control allows one to open up blocks of data on
a hardware component through processes without needing to know
anything about the structure of the way the files are organised on
that opened block at all.

The second is very simple: a character file allows the interfacing of
the operating system with hardware that accepts character I/O,
say... serial modems or old-timey printers, routers... &c

### Pipes

Pipes allow processes to send information to one-another by tricking
them into thinkign that they are writing to files, when in fact the
operating system is directly 'piping' the information between them.

[A] === [B]

These two processes, for example, think they are writing out their
output to regular files in the file system, but actually they are
directly transmitting information between themselves. The processes
would have to submit a system call in order to discover this greater
amount of contextual information about how they are operating.

## The Shell

It is, in fact, not a part of the operating system at all. It does,
make heavy use of a great number of the features of an operating
system. 

Comment from Vidak: ((It is also the objectively correct way to
interface with a computer system. If you disagree you are wrong and
should feel bad. Go home and rethink your life C; ))

## System Calls

Tanenbaum: "It is useful to remember: single CPUs can only execute one
instruction at a time. If a process is running a user program in user
mode and needs a system service, such as reading data from a file, it
has to execute a trap or system call instruction to transfer control
to the operating system in order to complete this task.

The operating system then inspects the parameters of the calling
process in order to work out what it wants.

Speaking broadly and generally, this is the process through which a
process makes a system call to the operating system:

  * The operating system carries out the system call, after taking
    over control from it, and then returns CPU control to the
    instruction that made the call.
  * Frequently, however, processes make "procedure calls", and not
    system calls in order to complete tasks. A procedure call is is
    the same as a system call, except that procedure call execution
    does not enter the kernel/superuser mode in order to complete the
    request that a process has made.
	
### MINIX System Calls

As a general rule, MINIX is highly conformant with POSIX
standards. However, the mapping of MINIX system calls onto POSIX
procedure calls is not always necessarily 1:1. The POSIX standard
specifies a number of procedures that a conformant system must supply,
but it does not specify/require them to be system calls, library
calls, or something else.

In some cases, the POSIX procedures are supported as library routines
in MINIX 3. In roders, several required procedures are only minor
variations of one-another, and one system call handles all of them.

### An Exhaustive List of MINIX 3's System Calls

There are exactly 53 fundamental system calls in the MINIX operating
system. They are divided up into exactly six categories. These are the
six categories:

  * Process Management
  * Signals
  * File Management
  * Directory and File System Management
  * Protection
  * Time Management
  
Comment from Vidak:

> My decision to include a complete list of all the basic system calls
> in MINIX that are written in Chapter One is because having some
> familiarity with any or all of them is very enlightening and
> informative. Each of these system calls is conformant with some
> critical requirement in the POSIX standard. This means just reading
> the names and descriptions of each of the system calls helps you learn
> the POSIX standard.

> As far as I am aware, a complete operating system, even if just a
> toy one, can be assembled by implementing all of these system
> calls. This is a very exciting fact to know. It means you can have a
> powerful working knowledge of operating systems just by knowing this
> small number of system calls (what is elsewhere called an API, in
> proprietary operating system documentation).

> To better aid memorisation or quick mental recall, I have added
> mneumonics next to each brief system call definition. The structure
> of the sections that follow is the following:

> X: SYSTEM CALL CODE
	> ("MNEUMONIC") SYSTEM CALL DEFINITION
	> 
	> DISCUSSION

#### 0 PROCESS MANAGEMENT

(Number of system calls: 10)

##### 0: pid = fork()

("FORK") Create a child process identical to the parent.

This is the only way to make a new process in MINIX 3. It creates an
exact duplicate of the original process, including all the file
descriptors, registers -- /everything/. After the fork, the original
process (parent) and the copy (child) go their separate ways. All the
variables have identical values at the time of the fork, but since the
parent's data are copied to create the child, subsequent changes in
one of them do nto affect the other -- however, at this stage, the
program text of both the parent and child are identical.

The fork call returns a value which is zero in the child and equal to
the child's PID in the parent. Using the returned PID, the two
processes can see which one is the parent, and which one is the child.

##### 1: pid = waitpid(pid, &statloc, opts)

("WAITPID") Wait for a child process to terminate.

In most cases, the child will need to execute different code than the
parent. This is where this system call is very important. This system
call is an instruction that the parent process sends to the operating
system. Its purpose is to request the operating system to suspend the
parent in order to wait for the completion of the execution of the
child process.

The address pointed to by the second parameter, *statloc*, will be set
to the child's exit status. The third parameter offers various other
options, and makes a little interesting extra reading.

##### 2: s = wait(&status)

("WAIT") Old version of waitpid(...)

##### 3: s = execve(name, argv, envp)

("EXECVE") Replace the entire core image of a process.

To affect some interesting consequence in the world, the child process
is somehow going to have to change its program code. This system call
achieves that purpose. It replaces the entire core image of the child
process. The new core image that the child process receives is the
first parameter of the system call, 'name'.

This is only the basic gist of how this flow works, however, because,
in MINIX it is actually a little more complex. The actual system call
that is performed to replace a process's core image is called 'exec',
and the system call written here is actually one of the subsequent
library calls that *exec* makes.

The extra complexity on this point is actually very good -- it means
you have many different parameters and options to consider when
forking.

This is a non-exhaustive list of the different library routines which
assist the primitive *exec* system call:

  * execl
  * execv
  * execle
  * execve

These different libraries are provided to allow the parameters of
*exec* to be omitted or specified in various ways. Generally,
throughout the MINX 3 book, these are all grouped together under the
abstract concept of *exec*.

In the msot general case of forking, *execve* has three parameters:

  * Name of the executable file with which to replace the child core
    image.
  * Pointer to the array of arguments to pass to *execve*.
  * Pointer to the environment array.
  
###### Demonstration

Consider a practical example. How does the operating system execute
the following shell command?

> cp file1 file2

The program code of *cp* is, lamentably, written in C, but its main
procedure looks like this:

> main(argc, argv, envp)

  * ARGC -> The number of items inputted to the command line.
  * ARGV -> A pointer to an array which allows one to select between
    the different number of command line items inputted. (For
    example, 

        Element *i* of that array is a pointer to the *i*-th string on
		the command line: ARGV[0] -> "cp"; ARGV[1] -> "file1", &c.
		
  * ENVP -> The third parameter of *cp*'s main procedure is a pointer
    to the environment, an array of strings containing assignments of
    the form *name* = *value*, which is used to pass information such
    as the terminal type and home directory name to a program.
	
So, when loading the *cp* program data into a child process's core
image, the operating system  will fill in all these variables for the
child process, so that it can execute the code, complete its program,
and then exit. All of this was triggered by the parent process's
request to the operating system for a forking of its process,
according to the parameters it passed along with the FORK system call.

What happens after the child process has completed the execution of
its program?

##### 4: exit(status)

("EXIT") Terminate the execution of a process and return an exit
status number.

The child process will pass an EXIT system call to the operating
system. This system call will pass a status value with its call,
which, in MINIX (and, I think this is POSIX conformant, so therefore
true for all UNIX operating systems), is *number* from 0 to 255 (i.e.,
$0000 to $FF - I refuse to use the notation '0xFF'). 

This exit status is actually passed to the parent process. It is
passed into the *&statloc* argument of its completed WAITPID system
call (see above).

If I am correct, *&statloc* is a 16-bit argument. The lower 8-bits of
the argument contains the termination status, with 0 being normal
termination and the other values being various error conditions. The
higher 8-bits contains the child's exit status.

Say, if a child process exits its execution with '4' as the parameter
to exit, the parent will be awakened by the operating system with *n*
set to the child's PID, and &statloc set to the constant $0400.

##### 5: size = brk(addr)

("SIZE"/"BRK") Set the size of the process's data segment (i.e., where
the process's variables are stored in RAM).

Now we can move onto a different topic: the anatomy of processes in
MINIX and POSIX systems. In MINIX, processes have their memory divided
up into three segments:

  * Text segment (Program code)
  * Data segment (Variables)
  * Stack segment 
  
Speaking generally, this illustration represent the memory map of a
typical process:

| STACK | (grows downwards) |
|:-----:|:-----------------:|
| *GAP* |                   |
| *GAP* |                   |
| DATA  | (grows upwards)   |
| TEXT  |                   |

As the process moves through execution, the data segment grows ever
upwards into memory, and the stack grows ever downwards. Between them
is unused memory/address space. 

The stack grows into the gap automatically, as needed. The expansion
of the data segment, however, is done explicitly through the use a
system called BRK (the title of this heading) which specifies the new
address where the data segment is to end.

This address may be more or less than the current value, however it is
*forbidden* to have the data segment become more than the stack.

BRK, and SBRK (the semi-automatic library for the BRK system call),
are however, **NOT** POSIX.

Usually, programmers, at time of this writing of the MINIX book (2008)
are encouraged to use *malloc*. Hilariously, *malloc* is not specified
in POSIX, because it was thought not necessary.

##### 6: pid = getpid()

("GETPID") Return caller's PID.

##### 7: pid = getpgrp()

("GETPGRP") Return ID of caller's process group.

##### 8: pid = setsid()

("SETSID") Create new 'session' and return its process group ID.

##### 9: l = ptrace(req, pid, addr, data)

("PTRACE") Used for debugging. There is a shell command called
ptrace. Running it yourself is completely safe, and it's a great way
to learn about how all this stuff works! :-)

#### 1 SIGNALS

(Number of system calls: 8)

When a signal is sent to a process that has not announced its
willingness to accept that signal, the process is unilaterally
'killed'. To avoid this fate, a process can use the SIGACTION system call:

##### 0: s = sigaction(sig, &act, &oldact)

("SIGACTION") Define the action that is to be taken on a transmitted
signal.

With this system call, a process can announce that it is prepared to
accept some signal type, and to provide the address of the signal
handling procedure and a place to store the address of the current
signal.

After a SIGACTION call, if a signal of the relevant type is generated,
the state of the process is pushed onto its own stack, and then the
signal handler is called. It may run for as long as it wants to, and
perform any system calls it wants.

When the signal handling is done, it calls SIGRETURN (immediately
below) to continue where it left off.

##### 1: s = sigreturn(&context)

("SIGRETURN") Return from a signal.

##### 2: s = sigprocmask(how, &set, &old)

("SIGPROCMASK") Examine or change the signal mask.

Signals can be blocked, by processes, but not indefinitely. 'Blocked'
signals are held pending until unblocked. This system call,
SIGPROCMASK, examines or manipulates a bitmap of 'a' or 'the' set of
current blocked system signals.

##### 3: s = sigpending(set)

("SIGPENDING") Find out the set of signals that are currently blocked.

A process can use _this_ system call to inquire and learn about the
pending set of signals that are currently undeliverable due to being
blocked. This information is returned as a bitmap.

##### 4: s = sigsuspend(sigmask)

("SIGSUSPEND") Replace the signal mask and suspend the selected
process.

Using _this_ system call, a process may suspend itself by _setting_
a bitmap of suspended system processes.

##### 5: s = kill(pid, sig)

("KILL") Send a signal to a process.

A signal can prevent subsequent types of signals from the operating
system with SIG_IGN, and can return to default action responses to
signals with SIG_DFL.

Vidak: ((I assume both of these variables manipulate the system bitmap
of signals.))

However, the default action is either to KILL a process or ignore the
signal, depending on which signal it is, in the current context.

Critically, there are virtually no processes can can ignore or capture
and 'block' the signal KILL when it is exercised unilaterally by the
operating system.

##### 6: residual = alarm(seconds)

("RESIDUAL") Set the alarm clock.

##### 7: s = pause()

("PAUSE") Suspend the caller until the next signal.

#### 2 FILE MANAGEMENT

(Number of system calls: 15)

#### 0: fd = creat(name, mode)

("CREAT") Obsolete way to create a new file.

#### 1: fd = mknod(name, mode, addr)

("MKNOD") Create regular, special, or directory i-node.

#### 2: fd = open(file, how, ...)

("OPEN") Open file for reading, writing, or both.

#### 3: s = close(fd)

("CLOSE") Close an open file.

#### 4: n = read(fd, buffer, nbytes)

("READ") Read data from file into buffer.

#### 5: n = write(fd, buffer, nbytes)

("WRITE") Write data from buffer into file.

#### 6: pos = lseek(fd, offset, whence)

("LSEEK") Move the file pointer information. (So, we're now pointing
somewhere else).

#### 7: s = stat(name, &buff)

("STAT") Get the file's status.

#### 8: s = fstat(fd, &buf)

("FSTAT") Get file's status information.

#### 9: fd = dup(fd)

("DUP") Allocate new file descriptor for open file.

#### 10: s = pipe(&fd[0])

("PIPE") Create pipe.

#### 11: s = ioctl(fd, request, argp)

("IOCTL") Perform special operations on a file.

#### 12: s = access(name, amode)

("ACCESS") Check a file's accessibility.

#### 13: s = rename(old, new)

("RENAME") Give a file a new name.

#### 14: s = fcntl(fd, cmd, ...)

("FCNTL") Lock a file, and other sorts of operations.

#### 3 DIRECTORY AND FILE SYSTEM MANAGEMENT

(Number of system calls: 9)

These system calls your average UNIX user would use perhaps 200 times
a week, so I will not spend time explaining them, as they are really a
part of basic UNIX literacy.

#### 0: s = mkdir(name, mode)
#### 1: s = rmdir(name)
#### 2: s = link(name, name2)
#### 3: s = unlink(name)
#### 4: s = mount(special, name, flag)
#### 5: s = umount(special)
#### 6: s = sync()
#### 7: s = chdir(dirname)
#### 8: s = chroot(dirname)

#### 4 PROTECTION

(Number of system calls: 7)

Again, all of this is a part of basic UNIX literacy. It is quite happy
that basic UNIX (shell) literacy is virtually immediate instruction
and familiarity with directly controlling the system kernel. There are
no intermediate metaphors, like the 'app store' or 'siri'/'cortana'.

#### 0: s = chmod
#### 1: uid = getuid()
#### 2: gid = setgid()
#### 3: s = setuid(uid)
#### 4: s = setgid(gid)
#### 5: s = chown(name, owner, group)
#### 6: oldmask = umask(complmode)

#### 5 TIME MANAGEMENT

(Number of system calls: 4)

#### 0: seconds = time(&seconds)

(Get elapsed time since 1970-01-01).

#### 1: s = stime(tp)

(Set elapsed time since 1970-01-01).

#### 2: s = utime(file, timep)

(Set file's 'last access' time).

#### 3: s = times(buffer)

(Get the user and system times used so far).

## Conclusion: Monolithic Operating Systems

Tanenbaum argues that monolithic operating systems effectively have no
structure.

These operating systems are an enormous bank which is a collection of
all the procedures that form the entire operating system.

Any procedure may call any other. The thing that does organise and
structure the monolithic operating system is that each procedure has
well defined interfaces, in terms of their paramters and expected
results. 

>"To construct the actual object project of the monolithic operating
>system when this approach is used, one:
>
>(1) First compiles all the individual procedures (or files
>containing the procedures)
>(2) Then binds them together into a single object file using the
>"system linker"

Monolithic kernels have essentially no "information binding". Every
procedure is visible to every other procedure. This is counterposed to
a structure where an operating system is organised into modules or
packages. This alternative structure has designated entry and exit
points for each module, and will otherwise conceal the rest of the
information about its operation.

Monolithic systems can have a little structure: the "services" or,
more POSIX-like, "system calls" are all provided and implemented by
structuring them in such a way that their paramters are placed in
well-known locations like, (a) certain registers; (b) the stack.

In monolithic systems, the supervisor call switches the computer from
user to kernel mode, and transfers control the user to the operating
system. Most CPUs are structured in this way: (userland/superuser
space).

### An Example System Call

Let us take this example system call, to illustrate this switching
between usermode and superuser mode:

> count = read(fd, buffer, nbytes);

  1. Push parameters nbytes, buffer, and fd onto the stack, in that
     order -- the reverse order. This is done by convention in C and
     C++ because it is convenient and desirable to make the first
     parameter to the format string PRINTF appear at the top of the
     stack. ((Don't worry, I don't understand either.))
	 
	 The parameters **fd** and **nbytes** are called by value, but
     **buffer** is caleld by reference -- which means the address of
     the buffer is passed, and not the actual value of the contents of
     the buffer.
	 
  2. We then call the library procedures which prepare the data for
     calling the operating system. This instruction is the normal
     procedure call instruction that we use to call all procedures in
     MINIX. The library is possibly written in ASM. The library puts
     the system call numebr in a place where the operating system
     expects it (for example, in some CPU register designated by
     convention).
  3. The TRAP instruction is then executed, and we switch from user
     mode to superuser mode. Execution is usually started a fixed
     address. 
  4. The kernel takes the system call binary or hex value, and
     examines it, and then dispatches it to the system call handler.
	 Usually this is done with a system of pointers to tables that
     would call the handlers of this particular system call number
     input. 
  5. The system call handler is selected by the pointer tables, and
     runs. 
  6. The system call handler finishes its work, and CPU control is now
     handed back to userspace library procedure that called this whole
     process. Execution is resumed at the exact instruction after the
     TRAP command.
  7. Return is called, and we're now back in the userland program that
     called the system call.
  8. The stack now needs to be cleaned up. The quick and dirty way to
     do this is usually to point the Stack Pointer where it will
     overwrite the old kernel system call and system call argument
     values.
	 
### Tanenbaum's Suggested Monolithic Operating System Structure

  1. A main userland program which invoked or executes the system call
     procedure.
  2. A set of service procedures which carry out the system calls.
  3. A set of utility procedures which help the system call
     procedures.
	 
For each system call you'd ideally have one service procedure. The
utility procedures then do things that many service procedures
require, like getting the right data from userland.

| MAIN PROGRAM | -> | CALLS KERNEL SERVICES USING SYSTEM CALLS | -> | UTILITIES | THAT DO WHAT THE KERNEL REQUIRES |

## FIN
