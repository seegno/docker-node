FROM mhart/alpine-node:4.2.6

# Add gcc and git support for native dependencies.
RUN apk add --update make gcc g++ python git && rm -rf /var/cache/apk/*

# Add a user to avoid running node as `root`.
RUN adduser -S node

# Change the working directory.
WORKDIR /home/node/app

# Workaround because `WORKDIR` always runs as root.
RUN chown -R node /home/node

# Change the user to avoid running as `root`.
USER node

# Install dependencies.
ONBUILD COPY *.json .
ONBUILD RUN npm install --ignore-scripts

# Setup node entrypoint.
ENTRYPOINT ["node"]
