# bela-torch

## Overview

This repository allows you to build torchlib for the Bela board (BeagleBone Black). Removing the need of building torch on the device itself.

The Dockerfile used in this repo is based on this other one https://github.com/XavierGeerinck/Jetson-Linux-PyTorch

## Requirements

- Docker
- A computer with a good CPU (building torch can take several hours)

## Building PyTorch

### Prerequisites

Before we get started we need to ensure that we can emulate ARM32. We do this by install `qemu` and configuring it:

```bash
# Install QEMU
sudo apt install binfmt-support qemu qemu-user-static

# Configure QEMU to enable execution of different multi-architecture containers by QEMU and binfmt_misc
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
```

### Building PyTorch

After our prerequisites are done, we can compile PyTorch by starting up the docker build process:

```bash
docker buildx build --platform=linux/arm/v7 --progress=plain --output type=local,dest=./pytorch-install --file Dockerfile.bela .
```

## References

Thanks a lot to the code repositories and authors below:

* https://github.com/XavierGeerinck/Jetson-Linux-PyTorch
