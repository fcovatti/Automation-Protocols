#lab04 Makefile. It should be the last to be called
TARGET := ../sim

#Include dirs
INCLUDE = ../include
PROC = ./termproc
UTIL = ./util
LIB = ../lib
SRC = $(PWD)

#flags
CFLAGS   := -O2 -Wall
CINCLUDE := -I$(UTIL) -I${INCLUDE} -I$(PROC)
CLIBDIR  :=
CLIBS    := -lm #-lpthread
DEPFLAGS := -MM

#includes
INCLUDE    = ${CINCLUDE}
FLAGS      = ${CFLAGS}
LIBDIR     = ${CLIBDIR}
LIBS       = ${CLIBS}
LIBINCLUDE = ${LIB}

#Setzen alle zusammen..
CMP      = gcc
LD       = ld
AR       = ar
ARFLAGS  = rvu
CMPFLAGS = ${FLAGS} ${INCLUDE}
LDFLAGS  = ${LIBS}

CSOURCES = $(wildcard *.c)
OBJECTS  = $(CSOURCES:.c=.o)
DEPS     = $(CSOURCES:.c=.d)
LIBFILES = $(PROC)/termproc.o $(UTIL)/frannor.o

#General
QUIET = @

.PHONY: clean install distclean clobber install

all: $(TARGET)

# The variable $@ has the value of the target and $^ has the value of the dependencies
# $< has the value of the first dependency file
$(TARGET): $(OBJECTS)
	$(QUIET)echo Compiling executable file: $@
	$(QUIET)${CMP} $(LDFLAGS) -o $@  $^ $(LIBFILES)

$(OBJECTS): $(CSOURCES)
	$(QUIET)echo Creating object: $@
	$(QUIET)$(CMP) $(CMPFLAGS) $(LIBS) -c $^

-include $(DEPS)
%.d: %.c
	$(QUIET)echo Creating dep: $@
	$(QUIET)$(CMP) $(DEPFLAGS) $(LIBS) $(CMPFLAGS) $< \
	| sed 's!\($*\)\.o[ :]*!\1.o $@ : !g' > $@; \
	[ -s $@ ] || rm -f $@

clean:
	$(QUIET)echo Removing temp and object files
	$(QUIET)rm -f *~ *.bak *.o

install:

distclean: clean
	$(QUIET)echo Removing executable and some unnecessary files
	$(QUIET)rm -f $(TARGET) $(DEPS) 
	$(QUIET) rm -f *.gch

clobber: distclean
# DO NOT DELETE
