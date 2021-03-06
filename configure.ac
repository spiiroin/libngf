AC_INIT(libngf/ngf.h)
AM_CONFIG_HEADER(config.h)
AC_CONFIG_MACRO_DIR([m4])

NGF_LIBRARY_NAME=libngf

NGF_MAJOR_VERSION=0
NGF_MINOR_VERSION=24
NGF_MICRO_VERSION=0

NGF_API_VERSION=1.0
AC_SUBST(NGF_API_VERSION)

NGF_LIBRARY_VERSION=1:1:1
AC_SUBST(NGF_LIBRARY_VERSION)

PACKAGE=$NGF_LIBRARY_NAME
AC_SUBST(NGF_LIBRARY_NAME)

NGF_VERSION=$NGF_MAJOR_VERSION.$NGF_MINOR_VERSION.$NGF_MICRO_VERSION
NGF_RELEASE=$NGF_MAJOR_VERSION.$NGF_MINOR_VERSION
AC_SUBST(NGF_VERSION)
AC_SUBST(NGF_RELEASE)

VERSION=$NGF_VERSION

AM_INIT_AUTOMAKE($PACKAGE, $VERSION, no-define)

AC_PROG_CC
AC_PROG_CXX
AM_PROG_CC_C_O
AM_PROG_LIBTOOL
AM_SANITY_CHECK

PKG_CHECK_MODULES(BASE, dbus-1)
AC_SUBST(BASE_LIBS)
AC_SUBST(BASE_CFLAGS)

PKG_CHECK_MODULES(GLIB, glib-2.0 dbus-glib-1)
AC_SUBST(GLIB_LIBS)
AC_SUBST(GLIB_CFLAGS)

PKG_CHECK_MODULES(CHECK, check)
AC_SUBST(CHECK_LIBS)
AC_SUBST(CHECK_CFLAGS)

AC_ARG_ENABLE([coverage],
	AS_HELP_STRING([--enable-coverage],[Enable coverage @<:@default=false@:>@]),
	[case "${enableval}" in
		yes) coverage=true ; CHECK_CFLAGS="${CHECK_CFLAGS} -fprofile-arcs -ftest-coverage" ; CHECK_LIBS="${CHECK_LIBS} -lgcov" ;;
		no)  coverage=false ;;
		*) AC_MSG_ERROR([bad value ${enableval} for --enable-coverage]) ;;
	esac],
	[coverage=false])
AM_CONDITIONAL([COVERAGE], [test x$coverage = xtrue])

AC_SUBST(CHECK_LIBS)
AC_SUBST(CHECK_CFLAGS)

pkgconfigdir="\$(libdir)/pkgconfig"
AC_SUBST(pkgconfigdir)

servicesdir="`pkg-config --variable=session_bus_services_dir dbus-1`"
AC_SUBST(servicesdir)

CFLAGS="${CFLAGS} -D_GNU_SOURCE"
AC_SUBST(CFLAGS)

echo "
 == $PACKAGE $VERSION ==

    Compiler:               ${CC}
    CFLAGS:                 ${CFLAGS}
    Code coverage:          ${coverage}
"

AC_OUTPUT(Makefile libngf0.pc libngf/Makefile examples/Makefile tests/Makefile)
