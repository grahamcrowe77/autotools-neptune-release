ACLOCAL_AMFLAGS = -I m4

releases:
lib: $(PACKAGE_NAME).tar.gz
	tar xf $<

$(PACKAGE_NAME).tar.gz: $(PACKAGE_NAME).boot
	$(ERL) -noshell -run systools make_tar $(PACKAGE_NAME) -s erlang halt

$(PACKAGE_NAME).script $(PACKAGE_NAME).boot: $(PACKAGE_NAME).rel
	$(ERL) -noshell -s systools make_script $(PACKAGE_NAME) -s erlang halt

pkgbindir=$(pkgdatadir)/erts-$(ERLANG_ERTS_VER)/bin

dist_pkgbin_DATA = \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/run_erl \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/erl \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/beam.smp \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/epmd \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/erlexec \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/erl_child_setup \
  $(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/inet_gethost

$(top_builddir)/erts-$(ERLANG_ERTS_VER)/bin/%: $(ERLANG_ROOT_DIR)/erts-$(ERLANG_ERTS_VER)/bin/%
	$(MKDIR_P) $(@D) && cp -p $< $@

install-data-local: lib releases $(PACKAGE_NAME).config $(PACKAGE_NAME).sh
	$(MKDIR_P) $(DESTDIR)$(pkgdatadir)
	cp -vr lib $(DESTDIR)$(pkgdatadir)
	cp -vr releases $(DESTDIR)$(pkgdatadir)
	cp -v $(PACKAGE_NAME).config \
	  $(DESTDIR)$(pkgdatadir)/releases/$(PACKAGE_VERSION)
	sed -e "s#@DESTDIR@#$(DESTDIR)#g" $(PACKAGE_NAME).sh \
	  > $(DESTDIR)$(bindir)/$(PACKAGE_NAME).sh
	chmod +x $(DESTDIR)$(bindir)/$(PACKAGE_NAME).sh
	chmod +x $(DESTDIR)$(pkgbindir)/*

CLEANFILES = \
  neptune.boot \
  neptune.script \
  neptune.tar.gz

clean-local:
	rm -rf erts-$(ERLANG_ERTS_VER)
	rm -rf releases
	rm -rf lib
