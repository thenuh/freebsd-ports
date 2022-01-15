PORTNAME=	drone-runner-exec
DISTVERSIONPREFIX=	v
DISTVERSION=	1.0.0-beta.9
CATEGORIES=	devel

MAINTAINER=	noone@FreeBSD.org
COMMENT=	Drone pipeline runner that executes builds directly on the host machine

LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:no_targets
USE_GITHUB=	yes
GH_ACCOUNT=	drone-runners
GH_PROJECT=     ${PORTNAME}
GH_SUBDIR=      src/github.com/${GH_ACCOUNT}/${GH_PROJECT}

DAEMONARGS=	-S -l \$${drone_runner_exec_facility} -s \$${drone_runner_exec_priority} -T \$${name}

SUB_LIST+=	DAEMONARGS="${DAEMONARGS}"

USE_RC_SUBR=	${PORTNAME}

PLIST_FILES=	bin/${PORTNAME}


do-build:
	@cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} GOPATH=${WRKDIR} go install ${GO_BUILDFLAGS}

do-install:
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}

.include <bsd.port.mk>
