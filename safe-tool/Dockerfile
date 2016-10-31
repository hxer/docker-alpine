FROM alpine:3.4
MAINTAINER janes - https://github.com/hxer

ENV PACKAGES="\
  #build-base \
  #bash \
  #ca-certificates \
  python \
  python-dev \
  py-pip \
  git \
  curl \
  nmap \
"

ENV PY_PACKAGES="\
  sqlmap \
"

RUN apk add --update $PACKAGES && \
    pip install --upgrade pip && \
    pip install $PY_PACKAGES && \
    rm -f /var/cache/apk/*

RUN mkdir /root/tool/
WORKDIR /root/tool/

RUN git clone https://github.com/lijiejie/subDomainsBrute.git && \
    git clone https://github.com/maurosoria/dirsearch.git

CMD ["/bin/sh"]
