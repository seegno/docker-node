# seegno/node

A node docker image.

[![seegno/node][docker-pulls-image]][docker-hub-url]
[![seegno/node][docker-stars-image]][docker-hub-url]

## Usage

### How to use this image

Create a `Dockerfile` in the root of application directory:

```Dockerfile
FROM seegno/node:<tag>
```

Then simply run:

```sh
$ docker build -t node
$ docker run --rm -it node
```

## Image Variants

All of the images are based on [alpine-node](https://github.com/mhart/alpine-node).

The `seegno/node` image comes in multiple flavors. Only the major version is tracked as there is a linked dependency to [alpine-node](https://github.com/mhart/alpine-node) on Docker Hub.

All images come with a `yarn` variant (e.g. `seegno/node:<version>-yarn`, `seegno/node:<version>-onbuild`).

### `seegno/node:latest`

Tag that points to the latest node version available as part of `seegno/node:<version>-onbuild`.

### `seegno/node:<version>`

Targets a specific version branch of node (e.g. `7`) and is an alias for the `onbuild` variant.

### `seegno/node:<version>-slim`

Targets a specific version branch of node (e.g. `7`) using a `slim` profile:

- Installs build dependencies for native modules;
- Creates and assigns the working directory `/home/node` to the `node` user;
- Copies `package.json` and `npm-shrinkwrap.json` to the working directory if they exist.

### `seegno/node:<version>-onbuild`

Targets a specific version branch of node (e.g. `7`) using an `onbuild` profile:

- Installs build dependencies for native modules;
- Creates and assigns the working directory `/home/node` to the `node` user;
- Copies `package.json` and `npm-shrinkwrap.json` to the working directory if they exist;
- Installs packages.

### `seegno/node:<version>-test`

Targets a specific version branch of node (e.g. `7`) using a `test` profile:

- Installs build dependencies for native modules;
- Installs packages;
- Runs `npm test`.

## Supported Docker versions

This image is officially supported on Docker `v1.12.1`, with support for older versions provided on a best-effort basis.

## License

[License information](https://github.com/seegno/docker-node/blob/master/LICENSE) for the `seegno/node` docker project.

[docker-hub-url]: https://hub.docker.com/r/seegno/node
[docker-pulls-image]: https://img.shields.io/docker/pulls/seegno/node.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/seegno/node.svg?style=flat-square
