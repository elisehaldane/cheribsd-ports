PORTNAME=	xdg-user-dirs
DISTVERSION=	0.18
CATEGORIES=	devel
MASTER_SITES=	http://user-dirs.freedesktop.org/releases/

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Tool to help manage personal user directories
WWW=		https://freedesktop.org/wiki/Software/xdg-user-dirs/

LICENSE=	GPLv2 MIT
LICENSE_COMB=	multi
LICENSE_FILE_GPLv2=	${WRKSRC}/COPYING

OPTIONS_DEFINE=			DOCS
OPTIONS_DEFAULT=		DOCS
OPTIONS_SUB=			yes

BUILD_DEPENDS=	${LOCALBASE}/share/xsl/docbook/html/docbook.xsl:textproc/docbook-xsl

GNU_CONFIGURE=	yes
USES=		gettext gmake gnome iconv localbase:ldflags
USE_GNOME=	libxslt:build
LDFLAGS+=	${ICONV_LIB}

.include <bsd.port.options.mk>

.if !${PORT_OPTIONS:MDOCS}
CONFIGURE_ARGS+=	--disable-documentation
.endif

.include <bsd.port.mk>
