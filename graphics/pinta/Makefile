# $OpenBSD$

V =		1.5
COMMENT =	open source drawing/editing program modeled after Paint.NET
DISTNAME =	pinta-${V}
CATEGORIES =	graphics x11

HOMEPAGE =	http://pinta-project.com/
MAINTAINER =	Brian Callahan <bcallah@openbsd.org>

# MIT
PERMIT_PACKAGE_CDROM =	Yes

# The tarballs have a proper configure. GH checkout does not...
MASTER_SITES =	https://github.com/PintaProject/Pinta/releases/download/${V}/

MODULES =	devel/gettext \
		lang/mono \
		textproc/intltool

BUILD_DEPENDS =	devel/mono-addins \
		x11/mono-gtk2

RUN_DEPENDS =	devel/desktop-file-utils \
		devel/mono-addins \
		x11/gtk+2,-guic \
		x11/mono-gtk2

CONFIGURE_STYLE =	gnu

USE_GMAKE =	Yes

.include <bsd.port.mk>
