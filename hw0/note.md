### Note for HW 0: Executable

* Instruction: http://cs162.eecs.berkeley.edu/static/hw/hw0.pdf


* objdump -x wc

``` 

CS 162 Fall   HW 0:  Executable

You will see that it has several segments, names of functions and variables in your program correspond
to labels with addresses or values.  And the guts of everything is chunks of stu÷ithin segments.
While you are looking through the objdump try and think about the following questions and put the answers in the le objdump.txt
.
 
What le format is used for this binary?  And what architecture is it compiled for?

What are the names of segments you nd?
* [thinkhy@localhost hw0]$ ./map 
What segment contains
wc
(the function) and what is it's address?  (hint:  objdump -w wc | grep
wc)

	What about
main
?
_main  @ 4005ce
	How  do  these  correspond  to  what  you  observed  in  gdb  when  you  were  looking  at  the  loaded,
executing program?
recur @ 400586
	Do you see the stack segment anywhere?  What about the heap?  Explain.
OK, now you are ready to write a program that reveals its own executing structure.  The second le
in hw0,
map.c
provides a rather complete skeleton.  You will need to modify it to get the addresses that
you are looking for and get the type casts right so that it compiles without warning.  The output of the
solution looks like the following (the addresses will be diㄦent).
precise64   hw0  ./map
Main  @ 40058c
recur @ 400544
Main stack: 7fffda11f73c
static data: 601028
Heap: malloc 1: 671010
Heap: malloc 2: 671080
recur call 3: stack@ 7fffda11f6fc
recur call 2: stack@ 7fffda11f6cc
recur call 1: stack@ 7fffda11f69c
recur call 0: stack@ 7fffda11f66c
Now think about the following questions and put the answers in
map.txt
.
_main stack: 7ffdcde6ec4c
	Using  objdump  on  the  map  executable.   Which  of  the  addresses  from  the  previous  section  are
dened in the executable, and which segment is each dened in?
static data: 60103c
	Make a list of the important segments, and what they are used for.
Heap: malloc 1: ebd010
	What direction is the stack growing in?
Heap: malloc 2: ebd080
	How large is the stack frame for each recursive call?
recur call -840504308: stack@ 7ffdcde6ec1c
	Where is the heap?  What direction is it growing in?
recur call -840504356: stack@ 7ffdcde6ebec
	Are the two
malloc()
ed memory areas contiguous?
recur call -840504404: stack@ 7ffdcde6ebbc
	Make  a  high  level  map  of  the  address  space  for  the  program  containing  each  of  the  important
segments, where they start and end, where the holes are, and what direction things grorecur call -840504452: stack@ 7ffdcde6eb8c

```

