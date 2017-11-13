## Docker binary installed in Ubuntu image

This allows to run the docker daemon inside an ubuntu container (Docker in Docker or just dind) and interact with it using Docker client binary.

## Usage

Run the daemon listening on particular port:

    docker run --rm --privileged --name docker-ubuntu-daemon \
        -it miminar/ubuntu-docker dockerd -H tcp://0.0.0.0:12345

**Note:** The port is exposed in the Dockerfile. If you want to make the daemon listen on different port, either rebuild the image with `--build-arg=PORT=54321` or append `--expose=54321` to the command line.

Then run the client on different terminal:

    docker run --rm -it \
        --link docker-ubuntu-daemon miminar/ubuntu-docker \
        /bin/sh -c 'docker -H "${DOCKER_UBUNTU_DAEMON_PORT_12345_TCP}" version'

Or exec into the container:

    docker exec -it docker-ubuntu-daemon docker version
