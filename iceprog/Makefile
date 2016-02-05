include ../config.mk

# iceprog seems to be compatible with libftdi-0.x and libftdi-1.x
ifeq (yes, $(shell pkg-config --exists libftdi1 && echo yes))
LIBFTDI=libftdi1
else
LIBFTDI=libftdi
endif

LDLIBS = `pkg-config --libs ${LIBFTDI}`
CFLAGS = -MD -O0 -ggdb -Wall -std=c99 `pkg-config --cflags ${LIBFTDI}`
MXEGCC = /usr/local/src/mxe/usr/bin/i686-pc-mingw32-gcc

all: iceprog

iceprog: iceprog.o

iceprog.exe: iceprog.c
	$(MXEGCC) -std=c99 -o iceprog.exe -Os iceprog.c

install: all
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	cp iceprog $(DESTDIR)$(PREFIX)/bin/iceprog

uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/iceprog

clean:
	rm -f iceprog
	rm -f iceprog.exe
	rm -f *.o *.d

-include *.d

.PHONY: all install uninstall clean

