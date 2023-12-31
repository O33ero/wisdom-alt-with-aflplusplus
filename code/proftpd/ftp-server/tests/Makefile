CC=gcc


top_builddir=..
top_srcdir=..
srcdir=.


include $(top_srcdir)/Make.rules

EXEEXT=

TEST_API_DEPS=\
  $(top_srcdir)/src/pool.o \
  $(top_srcdir)/src/privs.o \
  $(top_srcdir)/src/str.o \
  $(top_srcdir)/src/sets.o \
  $(top_srcdir)/src/timers.o \
  $(top_srcdir)/src/table.o \
  $(top_srcdir)/src/var.o \
  $(top_srcdir)/src/event.o \
  $(top_srcdir)/src/env.o \
  $(top_srcdir)/src/version.o \
  $(top_srcdir)/src/feat.o \
  $(top_srcdir)/src/netaddr.o \
  $(top_srcdir)/src/netacl.o \
  $(top_srcdir)/src/class.o \
  $(top_srcdir)/src/regexp.o \
  $(top_srcdir)/src/expr.o \
  $(top_srcdir)/src/scoreboard.o \
  $(top_srcdir)/src/stash.o \
  $(top_srcdir)/src/modules.o \
  $(top_srcdir)/src/cmd.o \
  $(top_srcdir)/src/response.o \
  $(top_srcdir)/src/fsio.o \
  $(top_srcdir)/src/netio.o \
  $(top_srcdir)/src/encode.o

TEST_API_LIBS=-lcheck

TEST_API_OBJS=\
  api/pool.o \
  api/array.o \
  api/str.o \
  api/sets.o \
  api/timers.o \
  api/table.o \
  api/var.o \
  api/event.o \
  api/env.o \
  api/version.o \
  api/feat.o \
  api/netaddr.o \
  api/netacl.o \
  api/class.o \
  api/regexp.o \
  api/expr.o \
  api/scoreboard.o \
  api/stash.o \
  api/modules.o \
  api/cmd.o \
  api/response.o \
  api/fsio.o \
  api/netio.o \
  api/stubs.o \
  api/tests.o


all:
	@echo "Running make from top level directory."
	cd ../; $(MAKE) all

dummy:

Makefile: Makefile.in ../config.status
	cd ../ && ./config.status

api/.c.o:
	$(CC) $(CPPFLAGS) $(CFLAGS) -c $<

api-tests$(EXEEXT): $(TEST_API_OBJS) $(TEST_API_DEPS)
	$(LIBTOOL) --mode=link --tag=CC $(CC) $(LDFLAGS) -o $@ $(TEST_API_DEPS) $(TEST_API_OBJS) $(LIBS) $(TEST_API_LIBS)
	./$@

running-tests:
	perl tests.pl

check-api: dummy api-tests$(EXEEXT)

check-commands:
	perl tests.pl --file-pattern '^t\/(commands\/|logins\.t)'

check-configs:
	perl tests.pl --file-pattern '^t\/config\/'

check-logging:
	perl tests.pl --file-pattern '^t\/logging\/'

check-modules:
	perl tests.pl --file-pattern '^t\/logging\/'

check-utils:
	perl tests.pl --file-pattern '^t\/utils\/'

check: check-api running-tests

clean:
	$(LIBTOOL) --mode=clean $(RM) *.o api/*.o api-tests$(EXEEXT) api-tests.log
