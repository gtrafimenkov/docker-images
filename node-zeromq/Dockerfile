FROM node:12.16.1-alpine3.11 as builder

RUN apk add --update --no-cache git autoconf automake make pkgconfig libtool gcc musl-dev g++ libunwind-dev

WORKDIR /opt

RUN git clone -n https://github.com/zeromq/libzmq.git && \
    cd libzmq && \
    git checkout e86237da5845cbe0a7da626e7eb1071a76464ce2

RUN cd libzmq && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install

FROM node:12.16.1-alpine3.11 as release

RUN apk add --update --no-cache musl libunwind

COPY --from=builder /usr/local/lib/ /usr/local/lib/
COPY --from=builder /usr/local/include/ /usr/local/include/
 
