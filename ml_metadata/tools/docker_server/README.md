Files for building the [Docker](http://www.docker.com) image for running the
MLMD gRPC server.

### Ubuntu

To build a docker image from Ubuntu, run
`./ml_metadata/tools/docker_server/build_docker_image.sh` under root directory
of github checkout.

### Fedora 38 and UBI9

To build from Fedora image, run
`DOCKER_FILE=Dockerfile.fedora ./ml_metadata/tools/docker_server/build_docker_image.sh` under root directory

Assure the `ZETASQL_COMMIT` == `f764f4e986ac1516ab5ae95e6d6ce2f4416cc6ff` in WORKSPACE file

### Fedora 39 and UBI8

To build from RedHat UBI image, run
`DOCKER_FILE=Dockerfile.redhat ./ml_metadata/tools/docker_server/build_docker_image.sh` under root directory

Assure the `ZETASQL_COMMIT` == `ac37cf5c0d80b5605176fc0f29e87b12f00be693` in WORKSPACE file
