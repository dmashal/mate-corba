check_PROGRAMS = client server

EVERYTHING_BUILT = \
	everything.h        \
	everything-skels.c  \
	everything-stubs.c  \
	everything-common.c

EVERYTHING_IDLOUT =          \
	$(EVERYTHING_BUILT)  \
	everything-imodule.c

AM_CPPFLAGS =                                 \
	-I$(top_srcdir)/include            \
	-I$(top_builddir)/include          \
	-I$(top_builddir)/src              \
	-I$(top_builddir)/src/MateCORBAutil    \
	-I$(top_srcdir)/src/orb            \
	-I$(top_srcdir)/src                \
	-I$(top_srcdir)/src/services/imodule \
	-DMATECORBA2_INTERNAL_API              \
        -DTEST_SRCDIR=\""$(top_srcdir)"/test/everything\" \
	$(WARN_CFLAGS)                     \
	$(LOCAL_LINC_CFLAGS)		   \
	$(MATECORBA_CFLAGS)			   \
	$(MATECORBA_IDL_CFLAGS)

#	-DMATECORBA_STUB_DEBUG_LOCAL

LDADD = $(top_builddir)/src/services/imodule/libMateCORBA-imodule-2.la	\
	$(top_builddir)/src/orb/libMateCORBA-2.la				\
	$(MATECORBA_IDL_LIBS)						\
	$(MATECORBA_LIBS)

#  -lefence

client.c : $(included_src)
	touch client.c
client_SOURCES=${EVERYTHING_BUILT} client.c everything.idl constants.h
client_DEPENDENCIES=${EVERYTHING_BUILT} $(included_src)
client_LDADD = $(LDADD)
client_LDFLAGS = -static -module

included_src = \
	anyServer.c	 \
	arrayServer.c    \
	basicServer.c    \
	contextServer.c  \
	deadReference.c  \
	lifeCycle.c	 \
	derivedServer.c  \
	pingServer.c     \
	sequenceServer.c \
	structServer.c   \
	unionServer.c

matecorbatypelibdir = $(libdir)/matecorba-2.0
matecorbatypelib_LTLIBRARIES = Everything_module.la

Everything_module_la_LDFLAGS = \
	-export-dynamic -module -no-undefined -avoid-version
Everything_module_la_SOURCES = \
	everything-imodule.c
Everything_module_la_LIBADD = \
        $(top_builddir)/src/orb/libMateCORBA-2.la \
	$(MATECORBA_LIBS)

server_SOURCES=server.c ${EVERYTHING_BUILT} everything.idl constants.h
server_LDFLAGS = -static -module
server.c : $(included_src)
	touch server.c
server_DEPENDENCIES=${EVERYTHING_BUILT} $(included_src)

IDL_FLAGS= --showcpperrors --add-imodule
IDL_FILES= everything.idl
include $(top_srcdir)/Makefile.shared

BUILT_SOURCES = ${EVERYTHING_BUILT} everything-imodule.c
CLEANFILES = ${BUILT_SOURCES} iorfile

TESTS = $(srcdir)/test.sh

EXTRA_DIST = $(IDL_FILES) test.sh $(included_src)

dist-hook:
	cd $(distdir); rm -f $(BUILT_SOURCES)
