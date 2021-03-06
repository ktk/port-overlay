# Created by: Anders F Bjorklund <afb@rpm5.org>
# $FreeBSD: head/sysutils/createrepo/Makefile 381587 2015-03-19 01:07:15Z skreuzer $

PORTNAME=	createrepo
PORTVERSION=	0.10.4
CATEGORIES=	sysutils
MASTER_SITES=	http://createrepo.baseurl.org/download/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Utility to create and manage RPM metadata repositories

LICENSE=	GPLv2

RUN_DEPENDS=	${PYTHON_SITELIBDIR}/sqlitecachec.py:${PORTSDIR}/devel/py-yum-metadata-parser@py27 \
		${PYTHON_SITELIBDIR}/libxml2.py:${PORTSDIR}/textproc/py-libxml2@py27 \
		${PYTHON_SITELIBDIR}/urlgrabber/__init__.py:${PORTSDIR}/www/py-urlgrabber@py27 \
		${PYTHON_SITELIBDIR}/yum/__init__.py:${PORTSDIR}/sysutils/yum \
		${PYTHON_SITELIBDIR}/deltarpm.py:${PORTSDIR}/sysutils/deltarpm@py27

USES=		gmake python:2.7 shebangfix
SHEBANG_FILES=	*.py */*.py Makefile

BUILD_DEPENDS+=	ginstall:${PORTSDIR}/sysutils/coreutils
GINSTALL=	ginstall

MAKE_ARGS=	MAKE=${MAKE_CMD} INSTALL="${GINSTALL} -p -v" PYTHON=${PYTHON_CMD} \
		prefix=${PREFIX} mandir=${MANPREFIX}/man sysconfdir=${PREFIX}/etc

post-patch:
	${FIND} ${WRKSRC} -type f | ${XARGS} \
	    ${REINPLACE_CMD} -e 's|/usr/share/createrepo|${DATADIR}|g'
	${REINPLACE_CMD} \
	    -e 's|$$(datadir)/$$(PKGNAME)|${DATADIR}|' \
	    -e '/^compdir :=/s|:= .*$$|= ${PREFIX}/share/bash-completion/completions|' \
	    ${WRKSRC}/Makefile
	${REINPLACE_CMD} -e '/^PYSYSDIR/s|:= \(.*\)|= ${PREFIX}|' \
	    ${WRKSRC}/createrepo/Makefile

.include <bsd.port.mk>
