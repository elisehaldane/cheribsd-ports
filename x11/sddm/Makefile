PORTNAME=	sddm
PORTVERSION=	0.20.0
DISTVERSIONPREFIX=	v
CATEGORIES=	x11

MAINTAINER=	kde@FreeBSD.org
COMMENT=	QML based login manager
WWW=		https://github.com/sddm/sddm

# The source code is GPLv2+, but the provided themes are:
#  - CC-BY 3.0 (default greeter theme, maldives)
#  - CC-BY 4.0 (maya)
#  - Apache20 (font included with maya)
LICENSE=	GPLv2+ CC-BY-3.0 CC-BY-4.0 APACHE20
LICENSE_COMB=	multi
LICENSE_FILE_GPLv2+ =	${WRKSRC}/LICENSE
LICENSE_FILE_CC-BY-3.0=	${WRKSRC}/LICENSE.CC-BY-3.0

OPTIONS_DEFINE=	DOCS
OPTIONS_SUB=	yes

OPTIONS_DEFAULT=	DOCS

DOCS_BUILD_DEPENDS=	rst2man.py-${PYTHON_VER}:textproc/py-docutils@${PY_FLAVOR}
RUN_DEPENDS=	dbus-run-session:devel/dbus \
		xauth:x11/xauth \
		xmessage:x11/xmessage

USES=		cmake compiler:c++11-lang cpe kde:5 pkgconfig qt:5 xorg
DOCS_USES=	python:build
CPE_VENDOR=	${PORTNAME}_project
USE_GITHUB=	yes
USE_KDE=	ecm:build
USE_QT=		core declarative dbus gui network \
		buildtools:build linguisttools:build declarative-test:build \
		qmake:build testlib:build
USE_XORG=	xau xcb

CONFLICTS_INSTALL=	lightdm

CMAKE_ARGS=	-DUID_MIN=1000 \
		-DUID_MAX=65000 \
		-DCMAKE_INSTALL_SYSCONFDIR:PATH=${LOCALBASE}/etc \
		-DSDDM_INITIAL_VT=7

DOCS_CMAKE_ON=	BUILD_MAN_PAGES
DOCS_CMAKE_ARGS=	-DRST2MAN_EXECUTABLE=${LOCALBASE}/bin/rst2man.py-${PYTHON_VER}

USE_RC_SUBR=	sddm
SUB_FILES=	xinitrc.desktop

USERS=		sddm
GROUPS=		sddm

post-patch:
	@${REINPLACE_CMD} -e 's#/etc/X11#${LOCALBASE}/etc/X11#' \
		-e 's#/usr/bin/#${LOCALBASE}/bin/#g' \
		-e 's#/usr/share/#${LOCALBASE}/share/#' \
		${WRKSRC}/data/scripts/Xsession \
		${WRKSRC}/src/common/Configuration.h
	@${REINPLACE_CMD} -e 's|/var/lib/AccountsService|/var/db/AccountsService|' \
		${WRKSRC}/src/greeter/UserModel.cpp

post-install:
# Install xsession.desktop to launch .xinitrc via sddm.
	${MKDIR} ${STAGEDIR}${PREFIX}/share/xsessions
	${INSTALL_DATA} ${WRKDIR}/xinitrc.desktop ${STAGEDIR}${PREFIX}/share/xsessions
	${INSTALL_SCRIPT} ${FILESDIR}/xinit-session ${STAGEDIR}${PREFIX}/share/sddm/scripts
	${REINPLACE_CMD} -e 's#@@LOCALBASE@@#${LOCALBASE}#' ${STAGEDIR}${PREFIX}/share/sddm/scripts/xinit-session
	${MV} ${STAGEDIR}${PREFIX}/etc/pam.d/sddm ${STAGEDIR}${PREFIX}/etc/pam.d/sddm.default
	${MV} ${STAGEDIR}${PREFIX}/etc/pam.d/sddm-autologin ${STAGEDIR}${PREFIX}/etc/pam.d/sddm-autologin.default
	${MV} ${STAGEDIR}${PREFIX}/etc/pam.d/sddm-greeter ${STAGEDIR}${PREFIX}/etc/pam.d/sddm-greeter.default

.include <bsd.port.mk>
