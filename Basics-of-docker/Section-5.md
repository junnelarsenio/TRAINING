# DISCOVERING DOCKER

### Hello world with Docker
- Type in the command line `docker run hello-world`
this command performed 4 key steps
  - 1. The Docker client contacted the Docker daemon.
  - 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
  - 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
  - 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
### Docker Image vs Docker Container

- `Docker Image` - is a combination of filesystem and parameters
  - No state and doesn't change
  - is something you can download, build and run
    
- `Docker Container` - are immutable
