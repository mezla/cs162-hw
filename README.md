# CS162 - 2015 Spring - Home Work

1. [HW0](https://gist.github.com/thinkhy/6f659c51d0f32ca4542c)
2. [HW1](https://gist.github.com/thinkhy/02ddbfb3f90ec21cb037)

### CS162 assignment -- first HomeWork HW0

PDF: http://cs162.eecs.berkeley.edu/static/hw/hw0.pdf

# 3.1 make

You have probably been using gcc to compile your programs, but this grows tedious and complicated
as the number of files you need to compile increases. You will need to write a Makefile that compiles
main.c, wc.c, and map.c. You will also need to write a target check that runs some sort of test that
will verify the output of wc and main. (You may do this any way you wish, but you MUST verify that
the output is existent and non-erroneous). It may also help to write a clean target (for make clean) to
remove your binaries. If all of this is new to you please read 2.2

# 3.2 wc

We are going to use wc.c to get you thinking once again in C, with an eye to how applications utilize
the operating system - passing command line arguments from the shell, reading and writing files, and
standard file descriptors. All of these things you encountered in CS 61C, but they will take on new
meaning in CS 162.

Your first task to write a clone of the unix tool wc, which counts the number of words inside a
particular text file. You can run unix’s wc to see what your output should look like, and try to mimic
its basic functionality in wc.c (don’t worry about the flags or spacing in the output).
While you are working on this take the time to get some experience with gdb. Use it to step through
your code and examine variables.

# 3.3 Executables and addresses
Now that you have dusted off your C skills and gained some familiarity with the CS 162 tools, we want
you to understand what is really inside of a running program and what the operating system needs to
deal with.
Load up your wc executable in gdb with a single input file command line argument, set a breakpoint
at wc, and run to there. Take a look at the stack using where or backtrace (bt).
While you are looking through gdb, think about the following questions and put your answers in the
file gdb.txt.

   * What is the value of infile? (hint: print infile)
   * What is the object referenced by infile? (hint: *infile)
   * What is the value of ofile? How is it different from that of infile? Why?
   * What is the address of the function wc?
   * Try info stack. Explain what you see.
   * Try info frame. Explain what you see.
   * Try info registers. Which registers are holding aspects of the program that you recognize?
    
   We have just peeled away the abstraction layers that is the onion of an executing program: the source
code, compiled into an object, linked into a executable, that is loaded and executed on a computer. The
operating system meets the application as an executable file when you run it. There is more to the
executable than meets the eye. Let’s look down inside.

    `objdump -x wc`

### 7CS 162 Fall 2014 HW 0: Executable

You will see that it has several segments, names of functions and variables in your program correspond
to labels with addresses or values. And the guts of everything is chunks of stuff within segments.
While you are looking through the objdump try and think about the following questions and put the
answers in the file objdump.txt.

   * What file format is used for this binary? And what architecture is it compiled for?
   * What are the names of segments you find?
   * What segment contains wc (the function) and what is it’s address? (hint: *objdump -w wc — grep
wc)
   * What about main?
   * How do these correspond to what you observed in gdb when you were looking at the loaded,
executing program?
   * Do you see the stack segment anywhere? What about the heap? Explain.

OK, now you are ready to write a program that reveals its own executing structure. The second file
in hw0, map.c provides a rather complete skeleton. You will need to modify it to get the addresses that
you are looking for and get the type casts right so that it compiles without warning. The output of the
solution looks like the following (the addresses will be different).


       precise64 hw0 ./map
       Main @ 40058c
       recur @ 400544
       Main stack: 7fffda11f73c
       static data: 601028
       Heap: malloc 1: 671010
       Heap: malloc 2: 671080
       recur call 3: stack@ 7fffda11f6fc
       recur call 2: stack@ 7fffda11f6cc
       recur call 1: stack@ 7fffda11f69c
       recur call 0: stack@ 7fffda11f66c

Now think about the following questions and put the answers in map.txt.
  
   * Using objdump on the map executable. Which of the addresses from the previous section are
defined in the executable, and which segment is each defined in?
   * Make a list of the important segments, and what they are used for.
   * What direction is the stack growing in?
   * How large is the stack frame for each recursive call?
   * Where is the heap? What direction is it growing in?
   * Are the two malloc()ed memory areas contiguous?
   * Make a high level map of the address space for the program containing each of the important
segments, where they start and end, where the holes are, and what direction things grow in.

### 8CS 162 Fall 2014 HW 0: Executable

## 3.4 user limits

The size of the dynamically allocated segments, stack and heap, is something the operating system has
to deal with. How large should these be? Poke around a bit to find out how to get and set user limits on
linux. Modify main.c so that it prints out the maximum stack size, the maximum number of processes,
and maximum number of file descriptors. Currently, when you compile and run main.c you will see it
print out a bunch of system resource limits (stack size, heap size, ..etc). Unfortunately all the values
will be 0! Your job is to get this to print the ACTUAL statistics. (Hint: man rlimit)

You should expect output similar to this:

     precise64 hw0 make
     precise64 hw0 ./main
     stack size: 8192
     process limit: 2782
     max file descriptors: 1024
     precise64 hw0 make check
     pass!
     precise64 hw0 echo $?
     0
     
## 3.5 autograder & submission

To push to autograder do:
    
      make clean
      git add .
      git commit -m "Trigger autograder."
      git checkout -b ag/hw0
      git push personal ag/hw0
      
This saves your work and it gives the instructors a chance to see the progress you are making.

Congratulations for not waiting till the last minute.

Within a few minutes you should receive an email from the autograder. (If not, please notify the
instructors via Piazza).

Now in order to finally submit your code, you need to push to the branch release/hw0.
    
      make clean
      git add .
      git commit -m "Submitting hw0."
      git checkout -b release/hw0
      git push personal release/hw0
  
The reason we gave you two types of branches with an autograder, is that the ag/* are testing
branches. Nothing on it will be graded. Whereas you must submit to release in order to get graded. So
please only push to release/* when you intend to submit.

Hopefully after this you are slightly more comfortable with your tools. You will need them for the
long road ahead!


# CS162-2015: HW1

   * [Official site](http://cs162.eecs.berkeley.edu)
   * [CS162 Spring 2015 Materials](http://cs162.eecs.berkeley.edu/static/spring2015/index.html)
   * [HW1](http://cs162.eecs.berkeley.edu/static/spring2015/hw/hw1.pdf) 
   * [Section 2: Processes](http://cs162.eecs.berkeley.edu/static/spring2015/sections/section2.pdf)
   * [Section 3: thread](http://cs162.eecs.berkeley.edu/static/spring2015/sections/section3.pdf)
   * [Implementing a Job Control Shell(Very useful)](http://www.gnu.org/software/libc/manual/html_node/Implementing-a-Shell.html#Implementing-a-Shell)
   * [My implementation on Github](https://github.com/thinkhy/ta/tree/master/hw1)

### HW 1: Initial Shell

 *Due: February 09, 2015*

### 1 Setup

The shell, e.g., bash, csh, or sh, is an application program that is so closely associated with the operating
system that most people think of it as part of the OS. But really the OS provides a clean abstraction for
accessing resources and manages sharing of those resources.  The shell provides a command interpreter
and the ability to run programs on the OS. (Your starter shell gives a little sense of this by getting and
printing its process id (PID) along with that of its parent - a real shell.)  In building one, you will get a
better sense of the user/system interface than you do from more typical applications.

``` shell
In your vagrant vm
cd code/personal
git pull staff master
cd hw1
```

You will find starter code shell.c and a simple Makefile.  You will notice the use of ".h" files to provide
a rough C approximation to classes.  A parser and a file for io operations have been included as well.

``` shell
In order to run the shell:
make
./shell
In order to terminate the shell after it starts, either type
quit
or press
ctrl-c
```

### 2  Using libc in the shell

The skeleton shell has a dispatcher to support 'builtins'.  This dispatch pattern shows up frequently in
operating systems; for example, it appears in vectoring syscalls to the appropriate kernel handler and in
vectoring interrupts to the interrupt handler.  Here we do a look up to transfer control to a command
handler.  So far the only two builtins supported are

``` shell
?
which brings up the help menu, and
quit
which exits from the shell.
```

Programs  normally  access  operating  capabilities  through  the  Standard  C  Library,  libc.   See,  for
example, http://www.gnu.org/software/libc/manual/pdf/libc.pdf.  To warm up, let's make this shell a
little more interesting.  Currently the prompt is just the command line number.  Modify this to include
the current working directory (see man getcwd) in the prompt.  Add a new built-in 'cd' that changes
the current working directory.  Test your program on all the relevant cases (and fix any bugs you may
find along the way.)

   Check in your solution to this part.  In your vagrant vm

``` shell
git add .
git commit -m "Finished adding libc functionality into the shell."
git push personal master
```

### TODO

   * currently the prompt is just the command line number.  Modify this to include
the current working directory (see man getcwd) in the prompt. 
   * add a new built-in 'cd' that changes the current working directory.  Test your program on all the relevant cases

### 3  A simple shell with Exec

You will notice that anything you type that is not a valid built-in results in a message that it doesn't
know how to exec programs.  Extend your shell of part 1 to fork a child process to execute the command
passing it the command line argument.  You may find the functions defined in parse.c to be useful for
parsing command line input.  In particular, you do not need to support delimiters not defined in parse.c
(eg.  quotes, escape characters).  For example:

```Shell
kubi@dhcp-45-107:~/Classes/cs162/sp15/cs162git/ta/hw1$  ./shell
./shell  running  as  PID  21799  under  17720
1  /Users/kubi/Classes/cs162/sp15/cs162git/ta/hw1:  /usr/bin/wc  shell.c
77         262       1843  shell.c
2  /Users/kubi/Classes/cs162/sp15/cs162git/ta/hw1:  quit
Bye
```

Your book provides a rough guideline.  Your shell should fork a child process which execs the exe-
cutable ﬁle. The parent shell process should wait until the subprocess completes.
Check in your solution to this part. In your vagrant vm

```shell
git  add  .
git  commit  -m  "Finished  creating  child  process  to  executes  files."
git  push  personal  master
```

### 4  Path resolution

You probably found that it was rather a pain to test your shell in the previous part because you had to
type the full pathname of every executable.  Most operating systems provide an "environment" in which
to resolve various names to their values.  For example

``` shell
 echo $PATH
```

prints the search path that the shell uses to locate executables.  It looks for the file in each directory on
the path, separated by ":" and executes the first one that it finds.  This process is called resolving the
path.
Modify your shell to access the PATH variable from the environment and use it to resolve executable
file names.  Typing in the full pathname of the executable should still be supported.  Do not use
execvp
.
Test your work and commit it.

### 5  Input/Output Redirection

When running programs, it is sometimes useful to be able to feed in input from a file or to write to a
file.  The syntax

 >[process] > [file]

specifies to write the process' output to the file.  Similarly, the
syntax
[process] < [file]
specifies to feed in the contents of the file into the process.  The commands

```C
dup2

and

strstr
```

may be useful here.
Modify your shell so that we support redirecting stdin and stdout.  Test your work and commit the
changes.

### 6  Process Bookkeeping

Not  only  do  we  want  our  shell  to  run  programs,  but  we  want  it  to  keep  track  of  programs  that  are
currently running, programs that have either been stopped or have terminated, and whether programs
hold the terminal or not. Modify your shell so that whenever your shell runs a program, it creates a
process struct and fills in its appropriate fields.  We have defined the process struct that you will be using for you.
Notice  that  we  are  not  exactly  changing  the  functionality  of  the  shell  at  the  moment,  but  this  is
necessary for supporting background processes and process control, as you will implement below.
You also want to make sure that when a process is stopped or is completed, that its data structure
is updated to reflect that.
Test your work and commit it.

### TODO
   * keep  track  of  programs  that  are currently running, programs that have either been stopped or have terminated
   * whenever your shell runs a program, it creates a process struct and fills in its appropriate fields.
 
### 7  Signal Handling

To interrupt/pause/stop running processes we will use libc's signals.  For example,

```
CTRL-C
sends
SIGINT
and
CTRL-Z
sends
SIGTSTP
```

However,  since our shell is running inside another shell,  by default these signals are sent to our shell.  This is not what we want, since for example attempting to stop a process will also stop our shell.  We want to "ignore" the signals inside our shell's process, and reenable them for the processes that our shell spawns.  Reading the linux man page for sigaction may be useful here.

You must also ensure that each process lies in its own process group.  A process group is a collection of one or more 
