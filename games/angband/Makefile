# $OpenBSD: Makefile,v 1.26 2012/04/11 16:16:33 edd Exp $
# Original from: Robert Ruehlmann

COMMENT=		rogue-like game with X11 support
COMMENT-no_x11=		rogue-like game

V =			3.4.1
V_DLDIR =		${V:C/\.[0-9]$//}
DISTNAME=		angband-v${V}
PKGNAME=		angband-${V}
CATEGORIES=     	games

HOMEPAGE=		http://rephial.org

MAINTAINER =		Edd Barrett <edd@openbsd.org>

# Multi license, including GPLv2, angband license, CC, freeware...
# The angband license contains the line "other copyrights may also apply"
PERMIT_PACKAGE_CDROM=	unclear license
PERMIT_PACKAGE_FTP=	Yes

WANTLIB=		c m ncursesw

MASTER_SITES =		${HOMEPAGE}/downloads/${V_DLDIR}/

AUTOCONF_VERSION =	2.68
CONFIGURE_STYLE=	autoconf

CONFIGURE_ARGS +=	--with-setgid=games \
			--bindir=${PREFIX}/bin

CONFIGURE_ENV=          TRUEPREFIX="${TRUEPREFIX}"
CONFIGURE_ENV +=	LDFLAGS=-L${LOCALBASE}/lib
USE_GMAKE =		Yes

FLAVORS=		no_x11 sdl
FLAVOR?=

.if ${FLAVOR:Mno_x11}
CONFIGURE_ARGS+=	--without-x
.else
CONFIGURE_ARGS+=	--with-x
WANTLIB+=		ICE SM X11
.endif

.if ${FLAVOR:Msdl}	# funky graphical mode and sounds
CONFIGURE_ARGS +=	--enable-sdl \
			--enable-sdl-mixer
PKG_ARGS +=		-Dsdl=1
LIB_DEPENDS +=		devel/sdl-mixer \
			devel/sdl-image \
			devel/sdl-ttf
RUN_DEPENDS +=		devel/desktop-file-utils
WANTLIB +=		SDL SDL_image SDL_mixer SDL_ttf pthread	
.else
CONFIGURE_ARGS +=	--disable-sdl-mixer	# defaults to ON
PKG_ARGS +=		-Dsdl=0
.endif

NO_TEST =		Yes

pre-configure:
	@perl -pi -e "s,/usr/share,${TRUEPREFIX}/share," \
		${WRKSRC}/lib/xtra/icon/angband*.desktop

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/applications
	mv ${PREFIX}/share/angband/xtra/icon/*.desktop \
		${PREFIX}/share/applications
	${INSTALL_DATA_DIR} ${PREFIX}/share/examples/angband/
	mv ${WRKINST}/etc/angband ${PREFIX}/share/examples/angband/etc

.include <bsd.port.mk>
