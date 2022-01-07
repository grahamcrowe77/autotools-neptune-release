ACLOCAL_AMFLAGS = -I m4

SUBDIRS = . tests

releases:
lib: $(PACKAGE_NAME).tar.gz
	tar xf $<

$(PACKAGE_NAME).tar.gz: $(PACKAGE_NAME).boot
	$(ERL) -noshell -run systools make_tar $(PACKAGE_NAME) -s erlang halt

$(PACKAGE_NAME).script $(PACKAGE_NAME).boot: $(PACKAGE_NAME).rel
	$(ERL) -noshell -s systools make_script $(PACKAGE_NAME) -s erlang halt

bin_SCRIPTS = \
  bin/$(PACKAGE_NAME).sh

pkgbindir=$(pkgdatadir)/erts-$(ERLANG_ERTS_VER)/bin

ERTS_MODS = \
  run_erl \
  erl \
  beam.smp \
  epmd \
  erlexec \
  erl_child_setup \
  inet_gethost

ERTS = $(addprefix $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/, $(ERTS_MODS))

dist_pkgbin_DATA = \
  $(ERTS) \
  $(top_builddir)/releases/$(PACKAGE_VERSION)/$(PACKAGE_NAME).config

$(top_builddir)/releases/$(PACKAGE_VERSION)/$(PACKAGE_NAME).config: $(PACKAGE_NAME).config
	$(MKDIR_P) $(@D) && cp -p $< $@

$(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/%: $(ERLANG_ROOT_DIR)/erts-$(ERLANG_ERTS_VER)/bin/%
	$(MKDIR_P) $(@D) && cp -p $< $@

all-local: lib

install-data-local:
	$(MKDIR_P) $(DESTDIR)$(pkgdatadir)
	cp -vr lib $(DESTDIR)$(pkgdatadir)
	cp -vr releases $(DESTDIR)$(pkgdatadir)
	cp -v $(PACKAGE_NAME).config \
	  $(DESTDIR)$(pkgdatadir)/releases/$(PACKAGE_VERSION)
	chmod +x $(DESTDIR)$(pkgbindir)/*

CLEANFILES = \
  neptune-release.boot \
  neptune-release.script \
  neptune-release.tar.gz

clean-local:
	rm -rf erts-$(ERLANG_ERTS_VER)
	rm -rf releases
	rm -rf lib
