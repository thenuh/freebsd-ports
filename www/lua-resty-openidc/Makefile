PORTNAME=	lua-resty-openidc
PORTVERSION=	1.7.4
DISTVERSIONPREFIX=	v
CATEGORIES=	www

MAINTAINER=	noone@freebsd.org
COMMENT=	OpenID Connect Relying Party and OAuth 2.0 Resource Server implementation in Lua for NGINX / OpenResty 

LICENSE=	BSD2CLAUSE

RUN_DEPENDS=	luajit-openresty>=2.1:lang/luajit-openresty \
		lua-resty-core>0:www/lua-resty-core \
		lua-resty-lrucache>=0.10:www/lua-resty-lrucache \
		lua-resty-session>=3.8:www/lua-resty-session \
		lua-resty-jwt>=0.2.3:www/lua-resty-jwt \
		lua-resty-http>=0.16.1:www/lua-resty-http \
		lua-resty-string>0:devel/lua-resty-string \
		lua51-cjson>0:devel/lua-cjson

USE_GITHUB=	yes
GH_ACCOUNT=	zmartzone

NO_ARCH=	yes
NO_BUILD=	yes

LUA_MODSHAREDIR=${LOCALBASE}/share/lua/5.1

PLIST_SUB=	LUA_MODSHAREDIR=${LUA_MODSHAREDIR}

do-install:
	@${MKDIR} ${STAGEDIR}${LUA_MODSHAREDIR}
	@(cd ${WRKSRC}/lib && ${COPYTREE_SHARE} . ${STAGEDIR}${LUA_MODSHAREDIR} "-name *\.lua")

.include <bsd.port.mk>
