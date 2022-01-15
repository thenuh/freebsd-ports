PORTNAME=	lua-resty-jwt
PORTVERSION=	0.2.3
DISTVERSIONPREFIX=	v
CATEGORIES=	www

MAINTAINER=	noone@freebsd.org
COMMENT=	JWT For The Great Openresty

LICENSE=	BSD2CLAUSE

RUN_DEPENDS=	luajit-openresty>=2.1:lang/luajit-openresty \
		lua-resty-openssl>=0.7.5:www/lua-resty-openssl

USE_GITHUB=	yes
GH_ACCOUNT=	cdbattags

NO_ARCH=	yes
NO_BUILD=	yes

LUA_MODSHAREDIR=${LOCALBASE}/share/lua/5.1

PLIST_SUB=	LUA_MODSHAREDIR=${LUA_MODSHAREDIR}

do-install:
	@${MKDIR} ${STAGEDIR}${LUA_MODSHAREDIR}
	@(cd ${WRKSRC}/lib && ${COPYTREE_SHARE} . ${STAGEDIR}${LUA_MODSHAREDIR} "-name *\.lua")

.include <bsd.port.mk>
