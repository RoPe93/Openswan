# Makefile for miscelaneous programs
# Copyright (C) 2002-2014  Michael Richardson	<mcr@sandelman.ca>
#
# This program is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by the
# Free Software Foundation; either version 2 of the License, or (at your
# option) any later version.  See <http://www.fsf.org/copyleft/gpl.txt>.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
# or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
# for more details.
#

OPENSWANSRCDIR?=$(shell cd ../..; pwd)
include ${OPENSWANSRCDIR}/Makefile.inc

ifeq ($(USE_LIBNSS),true)
CFLAGS+=-DHAVE_LIBNSS
ifeq ($(USE_FIPSCHECK),true)
FIPS_CHECK=1
CFLAGS+=-DFIPS_CHECK
endif
INCLUDES+=-I/usr/include/nspr4 -I/usr/include/nss3
endif

PROGRAM=rsasigkey
LIBS=${LIBOPENSWAN} ${LIBGMP}
ifeq ($(USE_LIBNSS),true)
LIBS+= -lnspr4 -lnss3 -lplc4
ifeq ($(USE_FIPSCHECK),true)
LIBS+=  -lfipscheck
endif
endif


include ${srcdir}../Makefile.program

# temp workaround for bug in nspr 4.8.2
ifeq ($(USE_LIBNSS),true)
CFLAGS+=-Wno-strict-prototypes
endif
