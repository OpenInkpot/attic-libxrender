dnl 
dnl  Copyright © 2003 Keith Packard, Noah Levitt
dnl 
dnl  Permission to use, copy, modify, distribute, and sell this software and its
dnl  documentation for any purpose is hereby granted without fee, provided that
dnl  the above copyright notice appear in all copies and that both that
dnl  copyright notice and this permission notice appear in supporting
dnl  documentation, and that the name of Keith Packard not be used in
dnl  advertising or publicity pertaining to distribution of the software without
dnl  specific, written prior permission.  Keith Packard makes no
dnl  representations about the suitability of this software for any purpose.  It
dnl  is provided "as is" without express or implied warranty.
dnl 
dnl  KEITH PACKARD DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE,
dnl  INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS, IN NO
dnl  EVENT SHALL KEITH PACKARD BE LIABLE FOR ANY SPECIAL, INDIRECT OR
dnl  CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE,
dnl  DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
dnl  TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
dnl  PERFORMANCE OF THIS SOFTWARE.
dnl
dnl Process this file with autoconf to create configure.

AC_PREREQ([2.57])

dnl
dnl Version should match the current Render version. XRenderQueryVersion
dnl returns the version from render.h, NOT the version we set here. But we
dnl try to keep these the same.  Note that the library has an extra
dnl digit in the version number to track changes which don't affect the
dnl protocol, so Xrender version l.n.m corresponds to protocol version l.n
dnl
AC_INIT(libXrender, 0.9.4, [https://bugs.freedesktop.org/enter_bug.cgi?product=xorg], libXrender)
AM_INIT_AUTOMAKE([dist-bzip2])
AM_MAINTAINER_MODE

AM_CONFIG_HEADER(config.h)

# Check for progs
AC_PROG_CC
AC_PROG_LIBTOOL

# Check for X
PKG_CHECK_MODULES(X, x11)
		  
X_REQUIRES="x11"
X_NON_PKG_CFLAGS=""
X_NON_PKG_LIBS=""

AC_SUBST(X_REQUIRES)
AC_SUBST(X_NON_PKG_CFLAGS)
AC_SUBST(X_NON_PKG_LIBS)

# Check render configuration, strip extra digits from package version to
# find the required protocol version

if test "$VERSION" = "" ; then
       VERSION=$PACKAGE_VERSION;
fi
RENDER_VERSION=[`echo $VERSION | sed 's/^\([0-9][0-9]*\.[0-9][0-9]*\).*$/\1/'`]
AC_SUBST(RENDER_VERSION)
PKG_CHECK_MODULES(RENDER, renderproto >= $RENDER_VERSION)

AC_SUBST(RENDER_CFLAGS)

XORG_CHECK_MALLOC_ZERO
XORG_RELEASE_VERSION

AC_OUTPUT([Makefile
	   src/Makefile
           xrender.pc])

