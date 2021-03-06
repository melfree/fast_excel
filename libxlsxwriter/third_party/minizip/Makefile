###############################################################################
#
# Simplied Makefile to build the minizip objects for the libxlsxwriter library.
#

# Keep the output quiet by default.
Q=@
ifdef V
Q=
endif

UNAME := $(shell uname)

# Change make and compiler options on AIX.
ifeq ($(UNAME), AIX)
CC = gcc
endif

# Check for MinGW/MinGW64/Cygwin environments.
ifneq (,$(findstring MINGW, $(UNAME)))
MING_LIKE = y
endif
ifneq (,$(findstring MSYS, $(UNAME)))
MING_LIKE = y
endif
ifneq (,$(findstring CYGWIN, $(UNAME)))
MING_LIKE = y
endif

FPIC = -fPIC
CFLAGS += -O3 -DNOCRYPT -DNOUNCRYPT

# Change make options on MinGW/MinGW64/Cygwin.
ifdef MING_LIKE
FPIC =
CC = gcc
CFLAGS += -DUSE_FILE32API
endif

# Fix for modified zconf.h on Gentoo.
ifneq (,$(findstring gentoo, $(UNAME)))
CFLAGS += -DOF=_Z_OF
endif

all: ioapi.o zip.o  ioapi.so zip.so

%.o  : %.c
	$(Q)$(CC)         -c $(CFLAGS) $<

%.so : %.c
	$(Q)$(CC) $(FPIC) -c $(CFLAGS) $< -o $@

clean:
	$(Q)/bin/rm -f *.o *.so
