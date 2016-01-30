# seegno/node

A node docker image.

[![seegno/node][docker-pulls-image]][docker-hub-url]
[![seegno/node][docker-stars-image]][docker-hub-url]
[![seegno/node][docker-size-image]][docker-hub-url]
[![seegno/node][docker-layers-image]][docker-hub-url]

## Usage

### How to use this image

Create a `Dockerfile` in the root of application directory:

```Dockerfile
FROM seegno/node:<version>
```

Then simply run:

```sh
$ docker build -t node
$ docker run --rm -it node
```

## Image Variants

The `seegno/node` image comes in a single flavor:

### `seegno/node:latest`

Tag that points to the latest node release available.

### `seegno/node:<version>`

Based on a [alpine-node](https://github.com/mhart/alpine-node) image, it targets a specific version branch of node (e.g. 5.5.0).

## Supported docker versions

This image is officially supported on docker version 1.9.1, with support for older versions provided on a best-effort basis.

## License

[License information](https://github.com/seegno/docker-node/blob/master/LICENSE) for the `seegno/node` docker project.

[docker-hub-url]: https://hub.docker.com/r/seegno/node
[docker-layers-image]: https://img.shields.io/imagelayers/layers/seegno/node/latest.svg
[docker-pulls-image]: https://img.shields.io/docker/pulls/seegno/node.svg
[docker-size-image]: https://img.shields.io/imagelayers/image-size/seegno/node/latest.svg
[docker-stars-image]: https://img.shields.io/docker/stars/seegno/node.svg
