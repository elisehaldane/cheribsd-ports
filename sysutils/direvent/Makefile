PORTNAME=	direvent
PORTVERSION=	5.3
CATEGORIES=	sysutils
MASTER_SITES=	GNU

MAINTAINER=	zeus@gnu.org.ua
COMMENT=	Per-directory file system event monitor
WWW=		https://www.gnu.org.ua/software/direvent/

LICENSE=	GPLv3+

USES=		gmake localbase
GNU_CONFIGURE=	yes
TEST_TARGET=	check
TEST_WRKSRC=	${WRKSRC}/tests

INFO=		${PORTNAME}

OPTIONS_DEFINE=	NLS
OPTIONS_SUB=	yes

NLS_USES=	gettext-runtime
NLS_CONFIGURE_OFF=	--disable-nls

.include <bsd.port.mk>
