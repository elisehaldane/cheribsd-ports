PORTNAME=	llhttp
PORTVERSION=	8.1.1
DISTVERSIONPREFIX=	 release/v
CATEGORIES=	www

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Port of http_parser to llparse
WWW=		https://llhttp.org/ \
		https://github.com/nodejs/llhttp

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE-MIT

USES=		cmake cpe

CMAKE_ON=	BUILD_SHARED_LIBS BUILD_STATIC_LIBS

PLIST_SUB=	PORTVERSION=${PORTVERSION} SHLIB_VER=${PORTVERSION:R}

GH_ACCOUNT=	nodejs
USE_GITHUB=	yes

.include <bsd.port.mk>
