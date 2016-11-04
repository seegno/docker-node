FROM mhart/alpine-node:base-4

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Add yarn.
ARG YARN_VERSION=v0.16.1

ENV PATH /usr/local/lib/yarn/bin/:$PATH

RUN apk --no-cache --virtual yarn-dependencies add ca-certificates openssl tar \
  && update-ca-certificates \
  && mkdir /usr/local/lib/yarn/ \
  && wget -O - https://github.com/yarnpkg/yarn/releases/download/${YARN_VERSION}/yarn-${YARN_VERSION}.tar.gz | tar -C /usr/local/lib/yarn/ --strip-components 1 -zxvf - \
  && apk del yarn-dependencies

# Add a user to avoid running node as `root`.
RUN adduser -S node

# Change the working directory.
WORKDIR /home/node/app

# Workaround because `WORKDIR` always runs as root.
RUN chown -R node /home/node

# Change the user to avoid running as `root`.
USER node

# Copy package.json and yarn.lock if they exist.
ONBUILD COPY *package.json *yarn.lock ./

# Setup node entrypoint.
ENTRYPOINT ["node"]
