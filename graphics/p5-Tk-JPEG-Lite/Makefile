PORTNAME=	Tk-JPEG-Lite
PORTVERSION=	2.01500
PORTREVISION=	3
CATEGORIES=	graphics perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-
DISTNAME=	${PORTNAME}-${PORTVERSION:S/00$//}

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Very simplistic image viewer that loads JPEG images
WWW=		https://metacpan.org/release/Tk-JPEG-Lite

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	p5-Tk>=0:x11-toolkits/p5-Tk

USES=		jpeg perl5
USE_PERL5=	configure

post-patch:
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|' \
		${WRKSRC}/Makefile.PL

.include <bsd.port.mk>
