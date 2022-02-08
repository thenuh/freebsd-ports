PORTNAME=	drone-server
DISTVERSIONPREFIX=	v
DISTVERSION=	2.9.1
CATEGORIES=	devel www

MAINTAINER=	noone@FreeBSD.org
COMMENT=	Drone is a Container-Native, Continuous Delivery Platform

LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:no_targets
USE_GITHUB=	yes
GH_ACCOUNT=	drone
GH_PROJECT=     drone
GH_SUBDIR=      src/github.com/${GH_ACCOUNT}/${GH_PROJECT}

GO_BUILDFLAGS+=	-tags "oss nolimit"

USERS=		www
GROUPS=		www

DAEMONARGS=	-S -l \$${drone_server_facility} -s \$${drone_server_priority} -T \$${name}
DRONE_DBDIR=	/var/db/drone_server

SUB_LIST+=	DAEMONARGS="${DAEMONARGS}" \
		DRONE_DBDIR="${DRONE_DBDIR}"


USE_RC_SUBR=	${PORTNAME}
SUB_FILES+=	${PORTNAME}.env.sample

PLIST_FILES=	bin/${PORTNAME}

PLIST_SUB=	DRONE_USER=${USERS} \
		DRONE_GROUP=${GROUPS} \
		DRONE_DBDIR=${GOGS_DBDIR}

do-build:
	@cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} GOPATH=${WRKDIR} go install ${GO_BUILDFLAGS} ./cmd/${PORTNAME}

do-install:
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}
	${MKDIR} ${STAGEDIR}${ETCDIR}
	${MKDIR} ${STAGEDIR}${DRONE_DBDIR}
	${INSTALL_DATA} ${WRKDIR}/${PORTNAME}.env.sample ${STAGEDIR}${ETCDIR}/${PORTNAME}.env.sample

.include <bsd.port.mk>
