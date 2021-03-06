# The way this file is written is a compromise between BSD make and GNU gmake.
# The original version was for BSD make, but other people complained that gmake
# outright refused to build it. For a while, there were two versions of the 
# makefile, one for each tool. This is a rewritten version that can satisfy both.

CC=avr-gcc
LIBDIR=lib
INCDIR=include
MCU=atmega16

CFLAGS=-Wall -Wextra -pedantic -std=iso9899:1999
CFLAGS+=-fno-builtin -Os -mcall-prologues 
CFLAGS+=-DF_CPU=8000000UL -DBAUD=9600U -mmcu=$(MCU) -I$(INCDIR)

all: libc

COBJFILES=fprintf.o panic.o fputs.o fgets.o fread.o fwrite.o hal.o

libc: $(COBJFILES)
	ar rc $(LIBDIR)/libc.a $(COBJFILES)
	@avr-ld -r $(COBJFILES) -o tmp.o
	avr-size -C --mcu=$(MCU) tmp.o
	@rm tmp.o

fgets.o: src/libc/stdio/fgets.c 
	$(CC) $(CFLAGS) -c $<

fprintf.o: src/libc/stdio/fprintf.c
	$(CC) $(CFLAGS) -c $<

fputs.o: src/libc/stdio/fputs.c
	$(CC) $(CFLAGS) -c $<

fread.o: src/libc/stdio/fread.c
	$(CC) $(CFLAGS) -c $<
	
fwrite.o: src/libc/stdio/fwrite.c
	$(CC) $(CFLAGS) -c $<

panic.o: src/libc/stdio/panic.c
	$(CC) $(CFLAGS) -c $<

hal.o: src/libc/stdio/hal.c
	$(CC) $(CFLAGS) -c $<

.PHONY: clean
clean:
	-rm *.o $(LIBDIR)/libc.a
