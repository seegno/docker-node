FROM node:5-alpine

# Add gcc and git support for native dependencies.
RUN apk --no-cache --virtual build-dependencies add g++ gcc git make python

# Change the working directory.
WORKDIR /app

# Install modules and run tests.
CMD ["sh", "-c", "npm install --unsafe-perm && npm test"]
