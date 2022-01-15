# freebsd-ports

## devel
+ drone-server
+ drone-runner-exec
+ drone-runner-ssh

## www 
+ lua-resty-http
+ lua-resty-jwt
+ lua-resty-openidc
+ lua-resty-openssl
+ lua-resty-session

## Notes
#### minimal example config for nginx \w openidc plugin (remember to build nginx \w lua [make config, check LUA option])
~~~
load_module "/usr/local/libexec/nginx/ndk_http_module.so";
load_module "/usr/local/libexec/nginx/ngx_http_lua_module.so";

worker_processes  1;

events {
  worker_connections 128;
}

http {

  lua_package_path '/usr/local/share/lua/5.1/ngx/?.lua;/usr/local/share/lua/5.1/resty/?.lua;;';
  lua_shared_dict discovery 1m;
  lua_shared_dict jwks 1m;

  resolver 8.8.8.8;

  lua_ssl_trusted_certificate /usr/local/share/certs/ca-root-nss.crt;
  lua_ssl_verify_depth 5;

  server {
    listen <port>;
    charset       utf-8;
    charset_types application/json;
    default_type  application/json;

    location / {

      access_by_lua_block {
          local cjson = require "cjson"
          local opts = {
             redirect_uri = "http://<my-app>/login",
             discovery = "http://<my-keycloak>:8080/auth/realms/<my-realm>/.well-known/openid-configuration",

             client_id = "<my-app-client-id",
             client_secret = "<my-app-client-secret>"

          }

          local res, err = require("resty.openidc").authenticate(opts)

          if err then
            ngx.status = 500
            ngx.say(err)
            ngx.exit(ngx.HTTP_INTERNAL_SERVER_ERROR)
          end

          ngx.status = 200
          ngx.say(cjson.encode(res))
          ngx.exit(ngx.HTTP_OK)

          -- ngx.req.set_header("X-USER", res.id_token.sub)
      }

      proxy_pass http://<my-app-backend>:<my-app-backend-port>;
    }
  }
}

~~~

