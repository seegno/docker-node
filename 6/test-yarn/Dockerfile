FROM node:6-alpine

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Add yarn.
RUN npm install -g yarn

# Change the working directory.
WORKDIR /app

# Install modules and run tests.
CMD ["sh", "-c", "yarn && yarn test"]
