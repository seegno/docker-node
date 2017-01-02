FROM node:6-alpine

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Change the working directory.
WORKDIR /home/node/app

# Workaround because `WORKDIR` always runs as root.
RUN chown -R node /home/node

# Change the user to avoid running as `root`.
USER node

# Copy package.json and npm-shrinkwrap.json if they exist.
ONBUILD COPY *.json ./

# Setup node entrypoint.
ENTRYPOINT ["node"]
