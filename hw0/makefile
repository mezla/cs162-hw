# CS162 HW0
SRCS=wc.c map.c main.c 

CC=gcc
CFLAGS=-g -Wall 
LDFLAGS=

OBJS=$(SRCS:.c=.o)
EXECUTABLES=$(basename $(SRCS))

all: $(EXECUTABLES)

%: %.o
	$(CC) $(CFLAGS) $<  $(LDFLAGS) -o $@  

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

check:
	verify.sh # TODO
clean:
	rm -rf $(EXECUTABLES) $(OBJS)
