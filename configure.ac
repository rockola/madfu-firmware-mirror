# Process this file with autoconf to produce a configure script
AC_PREREQ(2.0)
AC_INIT(madfuload, 1.2, [usb-midi-fw-user@lists.sourceforge.net])
AM_INIT_AUTOMAKE($PACKAGE_NAME, $PACKAGE_VERSION)
AC_REVISION($Revision$)
AC_CONFIG_SRCDIR(madfuload.c)
AC_PROG_CC

AC_MSG_CHECKING([for udev version])
udev_ver=`udevadm --version`
if test -n "$udev_ver"; then
  AC_MSG_RESULT([$udev_ver])
else
  AC_MSG_RESULT([none])
  udev_ver="0"
fi
if test "$udev_ver" -lt 057; then
  AC_MSG_ERROR([udev version 057 or later is required])
fi

AC_ARG_WITH([udev],
	    AS_HELP_STRING([--with-udev=dir],
			   [specify udev directory [[/etc/udev]]]),
	    [udev_dir="$withval"],
	    [udev_dir="/etc/udev"])
AC_CHECK_FILE([$udev_dir/udev.conf],
	      [udev_conf="$udev_dir/udev.conf"],
	      [udev_conf=""])

AC_MSG_CHECKING([for udev rules directory])
udev_rules=""
if test -r "$udev_conf"; then
  udev_rules=`. "$udev_conf"; echo "$udev_rules"`
fi
if test -n "$udev_rules"; then
  AC_MSG_RESULT([$udev_rules])
else
  udev_rules="$udev_dir/rules.d"
  AC_MSG_RESULT([not found; assuming $udev_rules])
fi
if test ! -d "$udev_rules"; then
  AC_MSG_ERROR([$udev_rules not found])
fi
AC_SUBST([UDEV_RULES_DIR], [$udev_rules])

AC_CONFIG_FILES(Makefile)
AC_OUTPUT
