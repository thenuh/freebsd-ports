PORTNAME=	drone-runner-ssh
DISTVERSIONPREFIX=	v
DISTVERSION=	1.0.1
CATEGORIES=	devel

MAINTAINER=	noone@FreeBSD.org
COMMENT=	Drone runner that executes a pipeline on a remote machine via ssh

LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:no_targets
USE_GITHUB=	yes
GH_ACCOUNT=	drone-runners
GH_PROJECT=     ${PORTNAME}
GH_SUBDIR=      src/github.com/${GH_ACCOUNT}/${GH_PROJECT}

DAEMONARGS=	-S -l \$${drone_runner_ssh_facility} -s \$${drone_runner_ssh_priority} -T \$${name}

SUB_LIST+=	DAEMONARGS="${DAEMONARGS}"

USE_RC_SUBR=	${PORTNAME}

PLIST_FILES=	bin/${PORTNAME}


do-build:
	@cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} GOPATH=${WRKDIR} go install ${GO_BUILDFLAGS}

do-install:
	${INSTALL_PROGRAM} ${WRKDIR}/bin/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}

.include <bsd.port.mk>
