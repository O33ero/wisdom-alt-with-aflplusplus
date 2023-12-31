

top_builddir=..
top_srcdir=..
srcdir=.


LS=/bin/ls


include ../Make.rules

CONTACT_ADDRESS=core@proftpd.org
COPYRIGHT_HOLDER="The ProFTPD Project"
PACKAGE=proftpd

# This file is generated using:
#
#   `find ../ -name "*.[ch]" -print | grep -v tests\/ | egrep "contrib|include|modules|src" | sort > files.txt'
#
# and is then checked into CVS.
FILES=files.txt

LANGS=bg_BG en_US es_ES fr_FR it_IT ja_JP ko_KR ru_RU zh_CN zh_TW $(EXTRA_LANGS)

# gettext utilities.  Note that this assumes gettext is installed and
# available on the system.
MSGCMP=msgcmp
MSGFMT=msgfmt
MSGINIT=msginit
XGETTEXT=xgettext

.SUFFIXES: .h

.PHONY: ""

all:
	@echo "Running make from top level directory."
	cd .. && $(MAKE) all

Makefile: Makefile.in ../config.status
	cd ../ && ./config.status

$(PACKAGE).pot:
	$(RM) $(PACKAGE).pot
	$(XGETTEXT) -L C --keyword=_ --flag=_:1:pass-c-format --keyword=N_ --flag=N_:1:pass-c-format --no-wrap --copyright-holder $(COPYRIGHT_HOLDER) --msgid-bugs-address $(CONTACT_ADDRESS) --sort-by-file -f $(FILES) -o $(PACKAGE).pot

locale: $(LANGS)

install: $(LANGS)
	for lang in $(LANGS); do \
		if [ -f $$lang.mo ]; then \
 			if [ ! -d $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES ]; then \
				mkdir -p $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES; \
				chown $(INSTALL_USER):$(INSTALL_GROUP) $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES; \
				chmod 0755 $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES; \
			fi; \
			$(INSTALL_MAN) $$lang.mo $(DESTDIR)$(localedir)/$$lang/LC_MESSAGES/$(PACKAGE).mo; \
		fi; \
	done

check:
	-for lang in $(LANGS); do \
		if [ -f $$lang.po ]; then \
			echo "Checking $$lang.po format..."; \
			$(MSGFMT) --check-format $$lang.po > /dev/null && echo "$$lang.mo OK"; \
			echo "Checking $$lang.po against template...."; \
			$(MSGCMP) $$lang.po $(PACKAGE).pot; \
			echo "----------------------"; \
		fi; \
        done

clean:
	$(RM) *.gmo *.mo 

$(LANGS):
	-if [ ! -f $@.po ]; then \
		$(MSGINIT) --no-translator -i $(PACKAGE).pot -o $@.po -l $@; \
	fi
	-if [ -f $@.po -a ! -f $@.mo ]; then \
		 $(MSGFMT) -o $@.mo $@.po; \
	fi
