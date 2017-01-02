FROM node:5-alpine

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

# Install dependencies.
ONBUILD COPY *package.json *yarn.lock ./
ONBUILD RUN yarn --ignore-scripts

# Copy project directory.
ONBUILD COPY . ./

# Change to `root` so we can change the ownership of the copied files.
ONBUILD USER root

# Change ownership to user `node`.
ONBUILD RUN chown -R node .

# Change the user to `node` to run the application.
ONBUILD USER node

# Rebuild packages.
ONBUILD RUN yarn

# Setup node entrypoint.
ENTRYPOINT ["node"]
