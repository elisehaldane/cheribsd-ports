PORTNAME=	juliamono
PORTVERSION=	0.048
CATEGORIES=	x11-fonts

MAINTAINER=	trueos@norwegianrockcat.com
COMMENT=	Monospaced typeface with many Unicode characters
WWW=		https://juliamono.netlify.app/

LICENSE=	OFL11

USES=		fonts xorg

USE_GITHUB=	yes
GH_ACCOUNT=	cormullion
GH_PROJECT=	juliamono
GH_TAGNAME=	1ef7ff0
USE_XORG=	x11
NO_ARCH=	yes
NO_BUILD=	yes

do-install:
	@${MKDIR} ${STAGEDIR}${FONTSDIR}
	${FIND} ${WRKSRC} -type f -name \*.ttf | while read f; do \
		${INSTALL_DATA} $$f ${STAGEDIR}${FONTSDIR} ; done

.include <bsd.port.mk>
