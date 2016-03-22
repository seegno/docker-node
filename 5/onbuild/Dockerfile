FROM mhart/alpine-node:5

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Add a user to avoid running node as `root`.
RUN adduser -S node

# Change the working directory.
WORKDIR /home/node/app

# Workaround because `WORKDIR` always runs as root.
RUN chown -R node /home/node

# Change the user to avoid running as `root`.
USER node

# Install dependencies.
ONBUILD COPY *.json ./
ONBUILD RUN npm install --ignore-scripts

# Copy project directory.
ONBUILD COPY . ./

# Change the user to `root` to remove build dependencies.
ONBUILD USER root

# Remove build dependencies.
ONBUILD RUN apk del build-dependencies

# Change the user to `node` to run the application.
ONBUILD USER node

# Setup node entrypoint.
ENTRYPOINT ["node"]
