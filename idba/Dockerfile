# kentwait/idba:latest
FROM kentwait/alpine-glibc-base
MAINTAINER Kent Kawashima <kentkawashima@gmail.com>

WORKDIR /tmp
RUN apk update && apk upgrade \
  && apk add --no-cache build-base \
  && apk add --no-cache --virtual temp-pkgs \
    git \
    autoconf \
    automake \ 
    sed \
  && git clone https://github.com/loneknightpy/idba.git \
  && cd /tmp/idba \
  && ./build.sh \
  && cp bin/idba /usr/local/bin/idba \
  && cp bin/idba_hybrid /usr/local/bin/idba_hybrid \
  && cp bin/idba_tran /usr/local/bin/idba_tran \
  && cp bin/idba_tran_test /usr/local/bin/idba_tran_test \
  && cp bin/idba_ud /usr/local/bin/idba_ud \
  && rm -rf /tmp/*
RUN git clone https://github.com/loneknightpy/idba.git \
  && cd /tmp/idba/src/ \
  && sed -i '102s/.*/    static const uint32_t kMaxShortSequence = 512;/' sequence/short_sequence.h \
  && sed -i '408s/.*/    if (median < 0 || median != median || sd != sd || sd > 10*median)/' release/idba_ud.cpp \
  && sed -i '410s/.*/        cout << "invalid insert distance. median " << median << " sd " << sd << endl;/' release/idba_ud.cpp \
  && sed -i '553s/.*/    if (median < 0 || median != median || sd != sd || sd > 10*median)/' release/idba_ud.cpp \
  && sed -i '555s/.*/        cout << "invalid insert distance. median " << median << " sd " << sd << endl;/' release/idba_ud.cpp \
  && sed -i '200s/.*/    static const uint32_t kNumUint64 = 16;/' basic/kmer.h \
  && cd /tmp/idba \
  && ./build.sh \
  && cp bin/idba /usr/local/bin/idba500 \
  && cp bin/idba_hybrid /usr/local/bin/idba_hybrid500 \
  && cp bin/idba_tran /usr/local/bin/idba_tran500 \
  && cp bin/idba_tran_test /usr/local/bin/idba_tran_test500 \
  && cp bin/idba_ud /usr/local/bin/idba_ud500 \
  && mkdir /data \
  && apk del temp-pkgs \
#  && rm -rf /tmp/* \
  && rm -rf /var/cache/apk/* \
            /opt/conda/pkgs/* \
            /root/.wget-hsts \
            /root/.[acpw]*

VOLUME /data
WORKDIR /data
ENTRYPOINT ["/init"]