FROM node:8-alpine

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Add yarn.
RUN npm install -g yarn

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
