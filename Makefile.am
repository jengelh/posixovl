# -*- Makefile -*-

AM_CPPFLAGS            = ${regular_CPPFLAGS}
AM_CFLAGS              = $(regular_CFLAGS) $(libfuse_CFLAGS)

man_MANS = posixovl.1

sbin_PROGRAMS          = mount.posixovl
EXTRA_PROGRAMS         = socket lntest
mount_posixovl_SOURCES = posixovl.c
mount_posixovl_LDADD   = $(libfuse_LIBS)

.PHONY: tarball
tarball:
	rm -Rf /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION};
	pushd ${top_srcdir} && git archive --prefix=${PACKAGE_TARNAME}-${PACKAGE_VERSION}/ HEAD | tar -C /tmp -x && popd
	pushd /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION} && ./autogen.sh && popd;
	tar -C /tmp --use=xz -cf ${PACKAGE_TARNAME}-${PACKAGE_VERSION}.tar.xz --owner=root --group=root ${PACKAGE_TARNAME}-${PACKAGE_VERSION}/
	rm -Rf /tmp/${PACKAGE_TARNAME}-${PACKAGE_VERSION};
