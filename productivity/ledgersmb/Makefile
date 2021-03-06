# $OpenBSD: Makefile.template,v 1.67 2013/07/10 15:22:23 bcallah Exp $

COMMENT=		financial accounting for small to medium size business

DISTNAME=		ledgersmb-1.3.37
CATEGORIES=		productivity
HOMEPAGE=		http://ledgersmb.org/

# GPLv2
PERMIT_PACKAGE_CDROM=		Yes

DISTFILES=		ledgersmb-1.3.37.tar.gz

MASTER_SITES+= \
	http://downloads.sourceforge.net/project/ledger-smb/ledgersmb/1.3.37/

WRKSRC=			${WRKDIR}/ledgersmb
WRKDIST=		${WRKSRC}

BUILD_DEPENDS=	${RUN_DEPENDS} \
				devel/p5-Module-Install

RUN_DEPENDS=	databases/postgresql,-server \
				databases/postgresql,-contrib \
				devel/p5-Log-Log4perl \
				devel/p5-Locale-Maketext-Lexicon \
				databases/p5-DBI \
				databases/p5-DBD-Pg \
				devel/p5-DateTime \
				www/p5-HTML-Template \
				www/p5-HTML-Tidy \
				www/p5-HTML-Tree \
				devel/p5-File-MimeInfo \
				www/p5-CGI-Simple \
				devel/p5-Error \
				textproc/p5-Template \
				mail/p5-MIME-Lite \
				devel/p5-Config-Std \
				math/p5-Math-BigInt-GMP

TEST_DEPENDS=	devel/p5-Test-Trap \
				devel/p5-Test-Exception \
				devel/p5-Test-Pod-Coverage \
				textproc/p5-Template-Plugin-Latex

# LWP tests require installation with Apache and PostgreSQL running.
# Database tests require PostgreSQL running.
# Must manually create role LSMB_ADMIN_USERNAME before database tests.
# CREATE ROLE root SUPERUSER CREATEDB CREATEROLE LOGIN ENCRYPTED PASSWORD 'pass';
TEST_FLAGS=		LSMB_TEST_DB=Yes
TEST_FLAGS+=	LSMB_NEW_DB=asshole
TEST_FLAGS+=	LSMB_ADMIN_USERNAME=root
TEST_FLAGS+=	LSMB_ADMIN_PASSWORD=pass
TEST_FLAGS+=	LSMB_ADMIN_FNAME=root
TEST_FLAGS+=	LSMB_ADMIN_LNAME=adminlast
TEST_FLAGS+=	LSMB_COUNTRY_CODE=US
TEST_FLAGS+=	PG_CONTRIB_DIR=/usr/local/share/postgresql/extension
TEST_FLAGS+=	PGUSER=postgres
TEST_FLAGS+=	PGPASSWORD=AcL54:!*
TEST_FLAGS+=	LSMB_TEST_LWP=Yes
TEST_FLAGS+=	LSMB_BASE_URL=http://127.0.0.1/ledgersmb/
TEST_FLAGS+=	LSMB_USER=root
TEST_FLAGS+=	LSMB_PASS=pass
TEST_FLAGS+=	LSMB_LOAD_COA=General.sql
TEST_FLAGS+=	LSMB_LOAD_GIFI=UCOA-Form990.sql
#TEST_FLAGS+=	PGDATABASE=asshole
#TEST_FLAGS+=	LSMB_SOURCE_DIR=/usr/ports/pobj/ledgersmb-1.3.33/ledgersmb

CONFIGURE_STYLE=perl

# Need to pick and choose files from messy distfiles
pre-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/ledgersmb
	cp -R ${WRKSRC}/doc/* \
		${WRKSRC}/README* \
		${WRKSRC}/COMPATIBILITY \
		${WRKSRC}/INSTALL \
		${WRKSRC}/COPYRIGHT \
		${WRKSRC}/UPGRADE \
		${WRKSRC}/BUGS \
		${WRKSRC}/CONTRIBUTORS \
		${PREFIX}/share/doc/ledgersmb
	rm ${PREFIX}/share/doc/ledgersmb/Notes.Ubuntu

	${INSTALL_SCRIPT_DIR} ${PREFIX}/share/ledgersmb/utils
	chmod -R 0755 ${WRKSRC}/utils/*/*pl
	cp -R ${WRKSRC}/utils/* ${PREFIX}/share/ledgersmb/utils
	rm ${PREFIX}/share/ledgersmb/utils/notify_short/GPL.txt

	${INSTALL_SCRIPT_DIR} ${PREFIX}/share/ledgersmb/tools
	chmod 0755 ${WRKSRC}/tools/*pl ${WRKSRC}/tools/*sh
	cp -R ${WRKSRC}/tools/* ${PREFIX}/share/ledgersmb/tools

	${INSTALL_SCRIPT_DIR} ${PREFIX}/share/ledgersmb/contrib
	chmod 0755 ${WRKSRC}/contrib/replication/configure-replication.sh
	cp -R ${WRKSRC}/contrib/* ${PREFIX}/share/ledgersmb/contrib

	${INSTALL_SCRIPT_DIR} ${PREFIX}/share/ledgersmb/drivers
	chmod 0755 ${WRKSRC}/drivers/pd3000.pl
	cp -R ${WRKSRC}/drivers/pd3000.pl ${PREFIX}/share/ledgersmb/drivers

	${INSTALL_DATA_DIR} ${PREFIX}/share/ledgersmb/web

	chmod 0644 ${WRKSRC}/LedgerSMB.pm
	chmod -R 0644 ${WRKSRC}/LedgerSMB/*pm
	chmod -R 0755 ${WRKSRC}/bin/*pl
	chmod -R 0755 ${WRKSRC}/scripts/*pl
	cp -R ${WRKSRC}/LedgerSMB \
		${WRKSRC}/UI \
		${WRKSRC}/bin \
		${WRKSRC}/css \
		${WRKSRC}/images \
		${WRKSRC}/locale \
		${WRKSRC}/scripts \
		${WRKSRC}/templates \
		${WRKSRC}/spool \
		${WRKSRC}/LedgerSMB.pm \
		${WRKSRC}/ledgersmb-httpd.conf.template \
		${WRKSRC}/ledgersmb.conf.default \
		${WRKSRC}/pos.conf.pl.template \
		${WRKSRC}/sql \
		${WRKSRC}/favicon.ico \
		${WRKSRC}/index.html \
		${PREFIX}/share/ledgersmb/web

	${INSTALL_SCRIPT} ${WRKSRC}/*pl ${PREFIX}/share/ledgersmb/web
	rm ${PREFIX}/share/ledgersmb/web/install_interactive.pl

# Need to keep manual pages but don't want perl files into P5SITE
do-install:
	rm -R ${WRKSRC}/*pl
	${INSTALL_MAN} ${WRKSRC}/blib/man3/* ${PREFIX}/man/man3p
	cp -R ${WRKSRC}/LedgerSMB* ${PREFIX}/${P5SITE}

.include <bsd.port.mk>
