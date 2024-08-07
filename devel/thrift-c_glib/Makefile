PORTNAME=	thrift
PORTVERSION=	${THRIFT_PORTVERSION} # to keep in sync with thrift
PORTEPOCH=	1
CATEGORIES=	devel
MASTER_SITES=	APACHE/thrift/${PORTVERSION}
DISTNAME=	thrift-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	C glib interface to Thrift
WWW=		https://thrift.apache.org/

PKGNAMESUFFIX=	-c_glib

BUILDIR=	${WRKDIR}/${DISTNAME}/lib/c_glib

DISTINFO_FILE=	${.CURDIR}/../thrift/distinfo

USES=		bison cmake compiler:c++11-lang cpe gnome libtool pathfix \
		pkgconfig ssl
CPE_VENDOR=	apache
CMAKE_ON=	BUILD_C_GLIB BUILD_SHARED_LIBS
CMAKE_OFF=	BUILD_CPP BUILD_HASKELL BUILD_JAVA BUILD_JAVASCRIPT \
		BUILD_NODEJS BUILD_PYTHON
USE_GNOME=	glib20
USE_LDCONFIG=	yes

.include "../thrift/bsd.thrift.mk"

PLIST_SUB+=	PORTVERSION="${PORTVERSION}"

.include <bsd.port.options.mk>

.if ( ${OPSYS} == FreeBSD && ${OSVERSION} >= 1400092 && ${SSL_DEFAULT} == base ) || ${SSL_DEFAULT:Mopenssl3*}
CXXFLAGS+=	-DOPENSSL_API_COMPAT=0x30000000L
.endif

post-patch:
	@${REINPLACE_CMD} 's,-Werror,,' ${WRKSRC}/compiler/cpp/Makefile.am \
		${WRKSRC}/lib/rb/ext/extconf.rb

.include <bsd.port.mk>
