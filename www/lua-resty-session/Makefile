PORTNAME=	lua-resty-session
PORTVERSION=	3.8
DISTVERSIONPREFIX=	v
CATEGORIES=	www

MAINTAINER=	noone@freebsd.org
COMMENT=	Session library for OpenResty – flexible and secure 

LICENSE=	BSD2CLAUSE

RUN_DEPENDS=	luajit-openresty>=2.1:lang/luajit-openresty		


USE_GITHUB=	yes
GH_ACCOUNT=	bungle

NO_ARCH=	yes
NO_BUILD=	yes

LUA_MODSHAREDIR=${LOCALBASE}/share/lua/5.1

PLIST_SUB=	LUA_MODSHAREDIR=${LUA_MODSHAREDIR}

do-install:
	@${MKDIR} ${STAGEDIR}${LUA_MODSHAREDIR}
	@(cd ${WRKSRC}/lib && ${COPYTREE_SHARE} . ${STAGEDIR}${LUA_MODSHAREDIR} "-name *\.lua")

.include <bsd.port.mk>
