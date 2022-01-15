PORTNAME=	lua-resty-openssl
PORTVERSION=	0.7.5
CATEGORIES=	www

MAINTAINER=	noone@freebsd.org
COMMENT=	FFI-based OpenSSL binding for OpenResty

LICENSE=	BSD2CLAUSE

RUN_DEPENDS=	luajit-openresty>=2.1:lang/luajit-openresty \
		openssl>=0:security/openssl

USE_GITHUB=	yes
GH_ACCOUNT=	fffonion

NO_ARCH=	yes
NO_BUILD=	yes

LUA_MODSHAREDIR=${LOCALBASE}/share/lua/5.1

PLIST_SUB=	LUA_MODSHAREDIR=${LUA_MODSHAREDIR}

do-install:
	@${MKDIR} ${STAGEDIR}${LUA_MODSHAREDIR}
	@(cd ${WRKSRC}/lib && ${COPYTREE_SHARE} . ${STAGEDIR}${LUA_MODSHAREDIR} "-name *\.lua")

.include <bsd.port.mk>
