FROM alpine:latest

LABEL MAINTAINER="Back Yu <yhfszb@gamil.com>"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# ENV SERVER_ADDR     0.0.0.0
# ENV SERVER_PORT     51348
# ENV PASSWORD        psw
# ENV METHOD          aes-128-ctr
# ENV PROTOCOL        auth_aes128_md5
# ENV PROTOCOLPARAM   32
# ENV OBFS            tls1.2_ticket_auth_compatible
# ENV TIMEOUT         300
# ENV DNS_ADDR        8.8.8.8
# ENV DNS_ADDR_2      8.8.4.4

ARG BRANCH=manyuser
ARG WORK=/root


RUN apk --no-cache add python libsodium wget \
	&& mkdir -p $WORK \
	&& wget -qO- --no-check-certificate https://github.com/shadowsocksr/shadowsocksr/archive/$BRANCH.tar.gz | tar -xzf - -C $WORK \
	&& cp -R $WORK/shadowsocksr-$BRANCH/shadowsocks $WORK/shadowsocks \
	&& rm -rf $WORK/shadowsocksr-$BRANCH

COPY user-config.json $WORK/shadowsocks/user-config.json
COPY usermysql.json $WORK/shadowsocks/usermysql.json

WORKDIR $WORK/shadowsocks

# CMD python server.py -p $SERVER_PORT -k $PASSWORD -m $METHOD -O $PROTOCOL -o $OBFS -G $PROTOCOLPARAM
CMD python server.py
