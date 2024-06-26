PORTNAME=	gcal
PORTVERSION=	4.1
PORTREVISION=	1
CATEGORIES=	deskutils
MASTER_SITES=	GNU

MAINTAINER=	ports@FreeBSD.org
COMMENT=	GNU Gregorian calendar program
WWW=		https://www.gnu.org/software/gcal/

LICENSE=	GPLv3+

GNU_CONFIGURE=	yes
CONFIGURE_ENV=	MAKEINFO="${MAKEINFO} --no-split"
USES=		charsetfix localbase shebangfix makeinfo tar:xz
SHEBANG_FILES=	misc/gcalltx/gcalltxp.in misc/gcalltx/gcalltx.pl

INFO=		gcal

OPTIONS_DEFINE=	NLS
OPTIONS_SUB=	yes
NLS_USES=		gettext
NLS_CONFIGURE_ENABLE=	nls

GCAL_SCRIPTS=	daily/daily ddiff/ddiff ddiff/ddiffdrv dst/dst gcalltx/gcalltx \
		gcalltx/gcalltxp moon/moon mrms/mrms srss/srss wloc/wlocdrv

post-patch:
.for p in ${GCAL_SCRIPTS}
	@${REINPLACE_CMD} -e '/^ThisGcal=/s:=.*:=${PREFIX}/bin/gcal:' \
		-e '/^packagedatamiscdir=/s:=.*:=${DATADIR}/misc/${p:H}:' \
		${WRKSRC}/misc/${p}.in
.endfor

post-install:
	@${TAR} -cf - -C ${WRKSRC} --exclude '*.in' --exclude '*.in.bak' \
		--exclude '*.alias' misc | \
		${TAR} -xpf - -C ${STAGEDIR}${DATADIR}
.for p in ${GCAL_SCRIPTS}
	@${CHMOD} +x ${STAGEDIR}${DATADIR}/misc/${p}
	@${LN} -s ../${DATADIR_REL}/misc/${p} ${STAGEDIR}${PREFIX}/bin/gcal-${p:T}
.endfor

.include <bsd.port.mk>
