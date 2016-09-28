FROM alpine:3.4

ENV VERSION=v7.0.0-nightly201609276b443d1731 NPM_VERSION=3

RUN apk add --no-cache curl make gcc g++ python linux-headers paxctl libgcc libstdc++ gnupg && \
  gpg --keyserver ha.pool.sks-keyservers.net --recv-keys \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 && \
  curl -o node-${VERSION}.tar.gz -sSL https://nodejs.org/download/nightly/${VERSION}/node-${VERSION}.tar.gz && \
  grep node-${VERSION}.tar.gz SHASUMS256.txt | sha256sum -c - && \
  tar -zxf node-${VERSION}.tar.gz && \
  cd node-${VERSION} && \
  export GYP_DEFINES="linux_use_gold_flags=0" && \
  ./configure --prefix=/usr ${CONFIG_FLAGS} && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  make -j${NPROC} -C out mksnapshot BUILDTYPE=Release && \
  paxctl -cm out/Release/mksnapshot && \
  make -j${NPROC} && \
  make install && \
  paxctl -cm /usr/bin/node && \
  cd / && \
  if [ -x /usr/bin/npm ]; then \
    npm install -g npm@${NPM_VERSION} && \
    find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; \
  fi && \
  apk del curl make gcc g++ python linux-headers paxctl gnupg ${DEL_PKGS} && \
  rm -rf /etc/ssl /node-${VERSION}.tar.gz /SHASUMS256.txt ${RM_DIRS} \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp /root/.gnupg \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Change the working directory.
WORKDIR /app

# Install modules and run tests.
CMD ["sh", "-c", "npm install --unsafe-perm && npm test"]
