CC=gcc


top_srcdir=..
srcdir=.


include ../Make.rules


all:
	@echo "Running make from top level directory."
	cd ../; $(MAKE) all

Makefile: Makefile.in ../config.status
	cd ../ && ./config.status

.c.o:
	$(CC) $(CPPFLAGS) $(CFLAGS) -c $<


src: $(OBJS) $(FTPDCTL_OBJS)

clean:
	rm -f *.o

depend:
	$(MAKEDEPEND) $(CPPFLAGS) *.c 2>/dev/null
	$(MAKEDEPEND) $(CPPFLAGS) -fMakefile.in *.c 2>/dev/null
