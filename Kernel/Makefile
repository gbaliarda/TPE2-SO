include Makefile.inc

# HEAP2 o BUDDY
MM=HEAP2

KERNEL=kernel.bin
SOURCES=$(wildcard *.c)
SOURCES_INTERRUPTIONS=$(wildcard interruptions/*.c)
SOURCES_UTILS=$(wildcard utils/*.c)
SOURCES_INTERRUPTIONS_ASM=$(wildcard interruptions/*.asm)
SOURCES_UTILS=$(wildcard utils/*.c)
SOURCES_ASM=$(wildcard asm/*.asm)
OBJECTS=$(SOURCES:.c=.o)
OBJECTS_INTERRUPTIONS=$(SOURCES_INTERRUPTIONS:.c=.o)
OBJECTS_UTILS=$(SOURCES_UTILS:.c=.o)
OBJECTS_INTERRUPTIONS_ASM=$(SOURCES_INTERRUPTIONS_ASM:.asm=.o)
OBJECTS_ASM=$(SOURCES_ASM:.asm=.o)
LOADERSRC=loader.asm

LOADEROBJECT=$(LOADERSRC:.asm=.o)
STATICLIBS=

ALL_OBJECTS= $(LOADEROBJECT) $(OBJECTS) $(OBJECTS_ASM) $(OBJECTS_INTERRUPTIONS) $(OBJECTS_UTILS) $(OBJECTS_INTERRUPTIONS_ASM)

all: $(KERNEL)

$(KERNEL): $(STATICLIBS) $(ALL_OBJECTS)
	$(LD) $(LDFLAGS) -T kernel.ld -o $@ $^

%.o: %.c
	$(GCC) $(GCCFLAGS) -D$(MM) -I./include -I./interruptions -c $< -o $@

%.o: %.asm
	$(ASM) $(ASMFLAGS) $< -o $@

$(LOADEROBJECT):
	$(ASM) $(ASMFLAGS) $(LOADERSRC) -o $(LOADEROBJECT)

clean:
	rm -rf $(ALL_OBJECTS) *.bin

.PHONY: all clean
