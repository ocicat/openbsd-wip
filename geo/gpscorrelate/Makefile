# $OpenBSD$

COMMENT =		EXIF geotagging

GH_ACCOUNT = 		freefoote
GH_PROJECT = 		gpscorrelate
GH_TAGNAME = 		1.6.1
GH_COMMIT = 		ea60215d88eaab43a8cdd8a15755b72af6c533d2
DISTNAME =		gpscorrelate-${GH_TAGNAME}

CATEGORIES =		geo x11

HOMEPAGE =		https://github.com/freefoote/gpscorrelate

MAINTAINER =		Kirill Bychkov <kirby@openbsd.org>

# GPLv2
PERMIT_PACKAGE_CDROM =	Yes

WANTLIB += GL X11 Xcomposite Xcursor Xdamage Xext Xfixes Xi Xinerama
WANTLIB += Xrandr Xrender atk-1.0 c cairo exiv2 expat fontconfig
WANTLIB += freetype gdk-x11-2.0 gdk_pixbuf-2.0 gio-2.0 glib-2.0
WANTLIB += gmodule-2.0 gobject-2.0 gthread-2.0 gtk-x11-2.0 m pango-1.0
WANTLIB += pangocairo-1.0 pangoft2-1.0 pixman-1 png pthread pthread-stubs
WANTLIB += stdc++ xcb xcb-render xcb-shm xml2 z

MODULES =		devel/gettext \
			textproc/intltool

BUILD_DEPENDS =		converters/xmltoman \
			textproc/docbook-xsl

LIB_DEPENDS =		graphics/cairo \
			graphics/exiv2 \
			textproc/libxml \
			x11/gtk+2

RUN_DEPENDS = 		devel/desktop-file-utils \
			x11/gtk+2,-guic

USE_GMAKE =		Yes
FAKE_FLAGS += 		mandir="${PREFIX}/man"

NO_TEST =		Yes

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/applications
	${INSTALL_DATA} ${WRKSRC}/gpscorrelate.desktop ${PREFIX}/share/applications/
	${INSTALL_DATA_DIR} ${PREFIX}/share/icons/hicolor/scalable/apps/
	${INSTALL_DATA} ${WRKSRC}/gpscorrelate-gui.svg ${PREFIX}/share/icons/hicolor/scalable/apps/


.include <bsd.port.mk>
