# Created by: Michael Vasilenko <acid@stu.cn.ua>
# $FreeBSD$

PORTNAME=	mp3blaster
PORTVERSION=	3.2.6
CATEGORIES=	audio
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-${PORTVERSION}

MAINTAINER=	novel@FreeBSD.org
COMMENT=	MP3 console ncurses-based player

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		gmake localbase:ldflags ncurses
GNU_CONFIGURE=	yes

OPTIONS_DEFINE=	DOCS ESOUND LIRC NAS SDL SIDPLAY VORBIS
OPTIONS_DEFAULT=	SIDPLAY VORBIS
SIDPLAY_DESC=	Sidplayer support

PORTDOCS=	AUTHORS CREDITS ChangeLog FAQ README TODO

LIRC_LIB_DEPENDS=		liblirc_client.so:comms/lirc
LIRC_CONFIGURE_WITH=		lirc

SIDPLAY_LIB_DEPENDS=		libsidplay.so:audio/libsidplay
SIDPLAY_CONFIGURE_WITH=		sidplay

VORBIS_LIB_DEPENDS=		libvorbisfile.so:audio/libvorbis
VORBIS_CONFIGURE_WITH=		oggvorbis

SDL_CONFIGURE_WITH=	sdl
SDL_USE=		SDL=yes

NAS_CONFIGURE_WITH=	nas
NAS_LIB_DEPENDS=	libaudio.so:audio/nas
NAS_LDFLAGS=		-laudio

ESOUND_CONFIGURE_WITH=	esd
ESOUND_USE=		GNOME=esound

post-patch:
	@${REINPLACE_CMD} -e 's|/usr/local/share/mp3blaster/win2koi.tbl|${DATADIR}/charmap/win2koi.tbl|' \
		${WRKSRC}/doc/sample.mp3blasterrc

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for i in ${PORTDOCS}
	@${INSTALL_DATA} ${WRKSRC}/${i} ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
