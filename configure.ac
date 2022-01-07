AC_PREREQ([2.69])
AC_INIT([neptune-release], [0.1.0], [graham.crowe@telia.com])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_SRCDIR([neptune-release.rel.in])
AM_INIT_AUTOMAKE([foreign subdir-objects])
AM_SILENT_RULES([yes])

AC_CONFIG_MACRO_DIRS([m4])
AC_CONFIG_TESTDIR([tests])
AC_CONFIG_FILES([tests/Makefile tests/atlocal])

# Checks for programs.
AC_ERLANG_NEED_ERL
AC_PROG_MKDIR_P

# Checks for libraries.
AC_ERLANG_SUBST_ROOT_DIR
AC_ERLANG_SUBST_ERTS_VER
erlang_erts_maj_ver=`echo $ERLANG_ERTS_VER | cut -d'.' -f1`
if test ${erlang_erts_maj_ver} -lt 10; then
  AC_MSG_ERROR([Erlang/OTP version must >= OTP-22.0!])
fi
AC_ERLANG_CHECK_LIB([kernel], [],
  [AC_MSG_ERROR([kernel was not found!])])
AC_ERLANG_CHECK_LIB([stdlib], [],
  [AC_MSG_ERROR([stdlib was not found!])])
AC_ERLANG_CHECK_LIB([sasl], [],
  [AC_MSG_ERROR([sasl was not found!])])
AC_ERLANG_CHECK_LIB([neptune], [],
  [AC_MSG_ERROR([neptune was not found!])])

if test "x${prefix}" == "xNONE"; then
  prefix=/usr/local
fi
exec_prefix="${prefix}"
bindir="${exec_prefix}/bin"
pkgdatadir="${bindir}/neptune"
AC_SUBST([pkgdatadir])

AC_CONFIG_FILES([Makefile ${PACKAGE_NAME}.rel])
AC_CONFIG_FILES([bin/neptune-release.sh], [chmod +x bin/neptune-release.sh])
AC_OUTPUT
cat << EOF
----------------------------------------------------------------------

${PACKAGE_NAME} Version ${PACKAGE_VERSION}

Prefix: '${prefix}'

Now type 'make @<:@<target>@:>@'
  where the optional argument <target> is:
    all                       - build all binaries
    check @<:@TESTSUITEFLAGS=-v@:>@ - run all tests @<:@verbose@:>@
    install                   - install everything
    installcheck              - test installation
----------------------------------------------------------------------
EOF
