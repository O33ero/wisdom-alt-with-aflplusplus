

top_builddir=..
top_srcdir=..
srcdir=.

GLUE_MODULE_OBJS=mod_core.o mod_xfer.o mod_rlimit.o mod_auth_unix.o mod_auth_file.o mod_auth.o mod_ls.o mod_log.o mod_site.o mod_delay.o mod_facts.o mod_ident.o  mod_cap.o
LTDLINCL=
SHARED_CFLAGS=-DPR_SHARED_MODULE
SHARED_LDFLAGS=-avoid-version -export-dynamic -module


include ../Make.rules

.SUFFIXES: .la

.PHONY: ""

all:
	@echo "Running make from top level directory."
	cd .. && $(MAKE) all

Makefile: Makefile.in ../config.status
	cd ../ && ./config.status

# Special instructions for mod_dso, to include the libltdl headers
mod_dso.o: mod_dso.c
	$(CC) $(CPPFLAGS) $(LTDLINCL) $(CFLAGS) -c mod_dso.c

.c.o:
	$(CC) $(CPPFLAGS) $(CFLAGS) -c $<

.c.la:
	$(LIBTOOL) --mode=compile --tag=CC $(CC) $(CPPFLAGS) $(CFLAGS) $(SHARED_CFLAGS) -c $*.c
	$(LIBTOOL) --mode=link --tag=CC $(CC) -o $@ -rpath $(LIBEXECDIR) $(LDFLAGS) $(SHARED_LDFLAGS) $*.lo `cat $(top_srcdir)/modules/$*.c | grep '$$Libraries:' | sed -e 's/^.*\$$Libraries: \(.*\)\\$$/\1/'`

module_glue.c: module_glue.c.tmpl $(STATIC_MODULE_OBJS)
	srcdir=$(srcdir) $(srcdir)/glue.sh $(GLUE_MODULE_OBJS)

shared: $(SHARED_MODULE_OBJS)
	@dirs="$(SHARED_MODULE_DIRS)"; \
	for dir in $$dirs; do \
		(cd $(top_srcdir)/$$dir/ && $(MAKE) shared); \
	done

static: $(STATIC_MODULE_OBJS) module_glue.o
	@dirs="$(STATIC_MODULE_DIRS)"; \
	for dir in $$dirs; do \
		module=`echo "$$dir" | sed -e 's/^.*\///'`; \
		(cd $(top_srcdir)/$$dir/ && $(MAKE) static) && \
		cp $(top_srcdir)/$$dir/$$module.o .; \
	done

install:
	test -z "$(SHARED_MODULE_OBJS)" || $(LIBTOOL) --mode=install --tag=CC $(INSTALL_BIN) $(SHARED_MODULE_OBJS) $(DESTDIR)$(LIBEXECDIR)
	@dirs="$(SHARED_MODULE_DIRS) $(STATIC_MODULE_DIRS)"; \
	for dir in $$dirs; do \
		(cd $(top_srcdir)/$$dir/ && $(MAKE) install); \
	done

clean:
	$(RM) *.a *.o module_glue.c
	$(LIBTOOL) --mode=clean $(RM) $(SHARED_MODULE_OBJS)
	$(LIBTOOL) --mode=clean $(RM) `echo $(SHARED_MODULE_OBJS) | sed 's/\.la$\/.lo/g'`
	@dirs="$(SHARED_MODULE_DIRS) $(STATIC_MODULE_DIRS)"; \
	for dir in $$dirs; do \
		(cd $(top_srcdir)/$$dir/ && $(MAKE) clean); \
	done

depend:
	$(RM) module_glue.c
	$(MAKEDEPEND) $(CPPFLAGS) *.c 2>/dev/null
	$(MAKEDEPEND) $(CPPFLAGS) -fMakefile.in *.c 2>/dev/null
