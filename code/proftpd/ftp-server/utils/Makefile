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

utils: $(FTPCOUNT_OBJS) $(FTPSCRUB_OBJS) $(FTPSHUT_OBJS) $(FTPTOP_OBJS) $(FTPWHO_OBJS)

clean:
	rm -f *.o

depend:
	$(MAKEDEPEND) $(CPPFLAGS) *.c 2>/dev/null
	$(MAKEDEPEND) $(CPPFLAGS) -fMakefile.in *.c 2>/dev/null
