FROM mhart/alpine-node:base-6

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

# Change the working directory.
WORKDIR /app

# Install modules and run tests.
CMD ["sh", "-c", "yarn && yarn test"]
