AC_PREREQ([2.62])
AC_INIT([heirloom-find], [0.0.20251121], [https://github.com/mpsuzuki/heirloom-find/-/issues])
AM_INIT_AUTOMAKE([foreign])

# Set default prefix
AC_PREFIX_DEFAULT(["/usr/ccs"])

# Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET

AC_HEADER_MAJOR
AC_CHECK_HEADERS([fnmatch.h mntent.h sys/param.h sys/mount.h sys/sysmacros.h sys/mkdev.h sys/statvfs.h])
save_CPPFLAGS="${CPPFLAGS}"
CPPFLAGS="${CPPFLAGS} -D_GNU_SOURCE"
have_gnu_extension=no

# open(2) flags
AC_CHECK_DECLS([O_DIRECT, O_DIRECTORY, O_NOATIME, O_NOFOLLOW, O_PATH, O_TMPFILE],
               [have_gnu_extensions=yes],[],[#include <fcntl.h>])

# math constants
AC_CHECK_DECLS([M_PI, M_E],
               [have_gnu_extensions=yes],[],[#include <math.h>])

# cpp macro functions
AC_CHECK_DECLS([strdupa, strndupa],
               [have_gnu_extensions=yes],[],[#include <string.h>])

# utility functions
AC_CHECK_FUNCS([getline getdelim mempcpy strcasestr qsort_r],
               [have_gnu_extensions=yes])
AC_CHECK_TYPES([struct mtget],[],[],[#include <sys/mtio.h>])
AC_CHECK_TYPES([struct floppy_struct],[],[],[#include <linux/fd.h>])

CPPFLAGS="${save_CPPFLAGS}"
if test "x${have_gnu_extensions}" = xyes
then
  AC_DEFINE([HAVE__GNU_SOURCE],[1],[-D_GNU_SOURCE enable some extensions])
fi

HEIRLOOM_FIND_LIBCOMMON
AS_IF([ test "x${build_included_libcommon}" = xyes ],
      [ AC_CONFIG_SUBDIRS( heirloom-libcommon ) ])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([GNUmakefile])
AC_OUTPUT
