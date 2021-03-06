
ACLOCAL_AMFLAGS = -I m4
WARNINGS = -Wall -Wwrite-strings -Werror
AM_CPPFLAGS = -I. -I$(srcdir)/src
AM_CFLAGS = $(WARNINGS) @libevent_CFLAGS@ @libcrypto_CFLAGS@
LDADD = libobfsproxy.a @libevent_LIBS@ @libcrypto_LIBS@ @ws32_LIBS@

bin_PROGRAMS = obfsproxy
noinst_LIBRARIES = libobfsproxy.a
noinst_PROGRAMS = unittests

libobfsproxy_a_SOURCES = \
	src/container.c \
	src/crypt.c \
	src/external.c \
	src/main.c \
	src/managed.c \
	src/network.c \
	src/protocol.c \
	src/socks.c \
	src/status.c \
	src/util.c \
	src/protocols/dummy.c \
	src/protocols/obfs2.c
if NEED_SHA256
libobfsproxy_a_SOURCES += src/sha256.c
endif

obfsproxy_SOURCES = src/obfs_main.c

unittests_SOURCES = \
	src/test/tinytest.c \
	src/test/unittest.c \
	src/test/unittest_container.c \
	src/test/unittest_crypt.c \
	src/test/unittest_socks.c \
	src/test/unittest_dummy.c \
	src/test/unittest_managed.c \
	src/test/unittest_obfs2.c

noinst_HEADERS = \
	src/container.h \
	src/crypt.h \
	src/external.h \
	src/ht.h \
	src/main.h \
	src/managed.h \
	src/network.h \
	src/protocol.h \
	src/sha256.h \
	src/socks.h \
	src/status.h \
	src/util.h \
	src/protocols/dummy.h \
	src/protocols/obfs2.h \
	src/test/tinytest.h \
	src/test/tinytest_macros.h

EXTRA_DIST = doc/obfs2/protocol-spec.txt

TESTS = unittests

doxygen:
	doxygen && cd doc/doxygen/latex && make

if HAVE_PYTHON
TESTS += tester.py
noinst_PROGRAMS += tester.py
tester_py_SOURCES = src/test/tester.py.in

tester.py: src/test/tester.py.in Makefile
	$(SED) -e 's,[@]PYTHON[@],$(PYTHON),' < src/test/tester.py.in > tester.py
	chmod +x tester.py
endif

man_MANS = doc/obfsproxy.1
