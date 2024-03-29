AC_INIT([posixovl], [1.3])
AC_PREREQ([2.61])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([config.h])
AC_PROG_INSTALL
AM_INIT_AUTOMAKE([-Wall foreign subdir-objects])
AC_PROG_CC
AM_PROG_CC_C_O

regular_CPPFLAGS="-D_LARGEFILE_SOURCE=1 -D_LARGE_FILES \
	-D_FILE_OFFSET_BITS=64 -D_REENTRANT";
regular_CFLAGS="-std=c99 -Wall -Waggregate-return \
	-Wmissing-declarations -Wmissing-prototypes -Wredundant-decls \
	-Wshadow -Wstrict-prototypes -Winline -pipe"
AC_SUBST([regular_CPPFLAGS])
AC_SUBST([regular_CFLAGS])

AC_CHECK_HEADERS([attr/xattr.h sys/xattr.h])

# FUSE >= 2.7.0 got subtype name support.
# 2.6.5 does not, but has a similar thing.
PKG_CHECK_MODULES([libfuse], [fuse >= 2.7.0], [], [
	PKG_CHECK_MODULES([libfuse], [fuse >= 2.6.5], [
		AC_DEFINE([HAVE_JUST_FUSE_2_6_5], [1],
			[Define if you have a FUSE version >= 2.6.5 but < 2.7.0])
	])
])

# Minium requirements for utimensat(): Linux 2.6.22-rc1 and Glibc 2.6
AC_MSG_CHECKING([for utimensat()])
#
# We need to check for __NR_utimensat too, because Glibc would
# offer a wrapper otherwise.
#
AC_LINK_IFELSE([AC_LANG_SOURCE([
		#define _ATFILE_SOURCE 1
		#include <sys/stat.h>
		#include <fcntl.h>
		#include <asm/unistd.h>
		static unsigned int x = __NR_utimensat;
		static int (*y)(int, const char *, const struct timespec *,
			int) = utimensat;
		int main(void) { return 0; }
	])], [
		AC_DEFINE([HAVE_UTIMENSAT], [1],
			[Define if utimensat() function is available])
		AC_MSG_RESULT([yes])
	], [
		AC_MSG_RESULT([no])
	])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
