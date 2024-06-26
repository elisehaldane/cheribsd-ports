PORTNAME=	qemu
PORTVERSION=	0.d${SNAPDATE}
PORTREVISION=	0
CATEGORIES=	emulators devel
PKGNAMESUFFIX=	-cheri

MAINTAINER=	brooks@FreeBSD.org
COMMENT?=	QEMU emulator with CHERI CPU support
WWW=		https://github.com/CTSRD-CHERI/qemu

DATADIR=	${PREFIX}/share/qemu-cheri

# XXX: disabling gnutls doesn't work so depend on it to avoid breakage.
BUILD_DEPENDS=	bash:shells/bash \
		meson>=0.57.1_1:devel/meson
LIB_DEPENDS=	libdrm.so:graphics/libdrm \
		libepoxy.so:graphics/libepoxy \
		libgnutls.so:security/gnutls \
		libnettle.so:security/nettle \
		libzstd.so:archivers/zstd

LICENSE=	GPLv2

USE_GITHUB=	yes
GH_TUPLE=	CTSRD-CHERI:qemu:${QEMU_COMMIT} \
		qemu:dtc:85e5d83:qemu_dtc/dtc \
		qemu:libslirp:8f43a99:qemu_libslirp/slirp \
		qemu:berkeley-softfloat-3:b64af41:qemu_berkeley_softfloat_3/tests/fp/berkeley-softfloat-3 \
		qemu:berkeley-testfloat-3:5a59dce:qemu_berkeley_testfloat_3/tests/fp/berkeley-testfloat-3 \
		qemu:keycodemapdb:6119e6e:qemu_keycodemapdb/ui/keycodemapdb \

HAS_CONFIGURE=	yes
MAKEFILE=	GNUmakefile
USES=		cpe gmake gnome ninja:build perl5 pkgconfig python:build xorg
USE_XORG=	pixman
USE_GNOME+=	glib20 libxml2
USE_PERL5=	build
USE_GL+=	gl
ONLY_FOR_ARCHS=	aarch64 amd64 powerpc64 powerpc64le

OPTIONS_DEFINE=	DOCS

.include "Makefile.snapshot"

CONFIGURE_ARGS+= \
		--target-list=riscv64cheri-softmmu,morello-softmmu \
		--enable-slirp=git \
		--disable-capstone \
		--disable-curl \
		--with-git-submodules=ignore \
		--disable-gtk \
		--disable-bsd-user \
		--disable-linux-user \
		--disable-linux-aio \
		--disable-kvm \
		--disable-opengl \
		--disable-vnc-jpeg \
		--disable-vnc-png \
		--disable-sdl \
		--disable-vte \
		--disable-xen \
		--prefix=${PREFIX} \
		--with-suffix=qemu-cheri \
		--firmwarepath=${DATADIR} \
		--meson=${LOCALBASE}/bin/meson \
		--smbd=${LOCALBASE}/sbin/smbd \
		--extra-cflags="-g ${EXTRA_CFLAGS}" \
		--localstatedir=/var
EXTRA_CFLAGS=	-DCHERI_UNALIGNED

.include <bsd.port.options.mk>

.if ${OPSYS} == FreeBSD && ( ${OSVERSION} >= 1400091 || ( ${OSVERSION} >= 1302507 && ${OSVERSION} < 1400000 ))
CFLAGS+=	-Wno-error=int-conversion
.endif

do-install:
	cd ${WRKSRC} && ${SETENV} DESTDIR=${STAGEDIR} ${GMAKE} install

.include <bsd.port.mk>
