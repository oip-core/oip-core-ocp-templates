FROM openresty/openresty:alpine-fat

RUN apk update && \
    apk add openssl && \
    apk add --virtual .build-dependencies openssl-dev git && \
    git config --global url."https://".insteadOf git:// && \
    luarocks install lua-resty-openidc && \
    apk del .build-dependencies && \
    ln -sf /dev/stdout /usr/local/openresty/nginx/logs/access.log && \
    ln -sf /dev/stderr /usr/local/openresty/nginx/logs/error.log && \
    mkdir /usr/local/openresty/nginx/client_body_temp && \
    chmod -vR g+wrX /usr/local/openresty/nginx/ 
    # following command doesn't work with busybox...
    # chmod -vR g+wrX /usr/local/openresty/nginx/{*_temp,logs}
    #chmod -vR g+wrX /usr/local/openresty/nginx/*_temp && \
    #chmod -vR g+wrX /usr/local/openresty/nginx/logs

ADD nginx* /

USER 1001
