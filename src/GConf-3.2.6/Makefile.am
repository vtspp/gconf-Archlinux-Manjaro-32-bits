
SUBDIRS = gconf backends po doc examples

DIST_SUBDIRS = tests gconf backends po doc examples defaults gsettings

if ENABLE_DEFAULTS_SERVICE
SUBDIRS += defaults
endif

if ENABLE_GSETTINGS_BACKEND
SUBDIRS += gsettings
endif

EXTRA_DIST =                \
	TODO                \
	gtk-doc.make        \
	intltool-update.in  \
	intltool-extract.in \
	intltool-merge.in

DISTCLEANFILES =          \
	intltool-update   \
	intltool-merge    \
	intltool-extract

DISTCHECK_CONFIGURE_FLAGS = --enable-gtk-doc --enable-introspection --enable-defaults-service --enable-gsettings-backend --disable-orbit

install-data-local:
	-mkdir -p $(DESTDIR)$(sysgconfdir)/gconf.xml.defaults
	-chmod 755 $(DESTDIR)$(sysgconfdir)/gconf.xml.defaults
	-mkdir -p $(DESTDIR)$(sysgconfdir)/gconf.xml.mandatory
	-chmod 755 $(DESTDIR)$(sysgconfdir)/gconf.xml.mandatory

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gconf-2.0.pc

aclocaldir = $(datadir)/aclocal
aclocal_DATA = gconf-2.m4

install-schemas:
	(cd standard-schemas && $(MAKE) $(AM_MAKEFLAGS) install-schemas)

dist-hook:
	@if test -d "$(srcdir)/.git"; \
	then \
		echo Creating ChangeLog && \
		( cd "$(top_srcdir)" && \
		  echo '# Generated by Makefile. Do not edit.'; echo; \
		  $(top_srcdir)/missing --run git log --stat ) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		     echo Failed to generate ChangeLog >&2 ); \
	else \
		echo A git clone is required to generate a ChangeLog >&2; \
	fi

