AM_CFLAGS = -Wall -Werror -Wextra -pedantic -fno-strict-aliasing
ACLOCAL_AMFLAGS = -I m4

#Shared library

lib_LTLIBRARIES = lib@PACKAGE_TARNAME@.la
lib@PACKAGE_TARNAME@_la_CPPFLAGS = -I$(top_srcdir)/include
lib@PACKAGE_TARNAME@_la_SOURCES = \
	src/data.c \
	src/device.c \
	src/error.c \
	src/monitor.c \
	src/timer.c \
	include/data.h \
	include/debug.h \
	include/device.h \
	include/driver.h \
	include/eml.h \
	include/error.h \
	include/monitor.h \
	include/timer.h

if ENABLE_MIC
lib@PACKAGE_TARNAME@_la_CPPFLAGS += -DENABLE_MIC
lib@PACKAGE_TARNAME@_la_SOURCES += src/driver-mic.c
endif

if ENABLE_RAPL
lib@PACKAGE_TARNAME@_la_CPPFLAGS += -DENABLE_RAPL
lib@PACKAGE_TARNAME@_la_SOURCES += src/driver-rapl.c
endif

if ENABLE_NVML
lib@PACKAGE_TARNAME@_la_CPPFLAGS += -DENABLE_NVML
lib@PACKAGE_TARNAME@_la_SOURCES += src/driver-nvml.c
endif

#Installed headers

include_HEADERS = include/@PACKAGE_TARNAME@.h
pkginclude_HEADERS = \
	include/@PACKAGE_TARNAME@/data.h \
	include/@PACKAGE_TARNAME@/device.h \
	include/@PACKAGE_TARNAME@/error.h

#Installed utilities

bin_PROGRAMS = \
	utils/consumed

#Test suite

binarytests = \
	test/device_query \
	test/monitor \
	test/nested \
	test/totals

LDADD = lib@PACKAGE_TARNAME@.la
AM_CPPFLAGS = -I$(top_srcdir)/include
check_PROGRAMS = $(binarytests)

TESTS = $(binarytests)

#Documentation

dist_doc_DATA = \
	README.md \
	doc/emlData.schema.json \
	doc/json.md \
	doc/usage.md

EXTRA_DIST = \
	Doxyfile.in \
	doc/groups.dox

include doc/doxygen.am
MOSTLYCLEANFILES = $(DX_CLEANFILES) $(DX_DOCDIR)

#Generated GNU files
GENGNUFILES =

GENGNUFILES += README
README:
	$(LN_S) README.md $@

GENGNUFILES += NEWS
NEWS:
	git for-each-ref 'refs/tags/v[0-9]*' --format="[@PACKAGE_NAME@ %(refname:short)] (released %(taggerdate:short))%0a%0a%(contents:body)%0a" > $@

GENGNUFILES += ChangeLog
ChangeLog:
	git log --pretty=format:"%ai %aN%n%n%x09* %s%d%n" > $@

DISTCLEANFILES = $(GENGNUFILES)
dist-hook: $(GENGNUFILES)