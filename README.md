# nginx:stable-alpine + proxy_connect module

Original work at
- [nginx:stable-alpine](https://github.com/nginxinc/docker-nginx/tree/master/stable/alpine)
- [ngx_http_proxy_connect_module](https://github.com/chobits/ngx_http_proxy_connect_module)

I removed gpg sig verification and debug version building for the sake of faster builds.

# Usage

It's on [Docker Hub](https://hub.docker.com/r/rpardini/nginx-proxy-connect-stable-alpine/); `:latest` is from master.

```bash 
docker run -it -p 8081:80 rpardini/nginx-proxy-connect-stable-alpine
```

- Just like `nginx:stable-alpine`, but you can use `proxy_connect;`.
- Also `proxy_connect_address $someVar;` is supported; this has the "rewrite" version of the patch
- you can map on `$connect_host`
- log `$connect_addr` for host:port of the final destination

# Why?

I wanted a more contained way of doing DNS overrides.

If you can convince a client program to use an https proxy, and inject your own CA certificate as trusted, 
you can use `proxy_connect` to send traffic to a second nginx server and do caching, filtering, rewriting, 
and who knows what else there.
