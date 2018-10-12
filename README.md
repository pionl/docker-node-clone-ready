# Docker image based on official node image with openssh and git installed

## Pre-installed packages:

- git and openssh-server for cloning support

## Tags:

- pionl/node-clone-ready:8
- pionl/node-clone-ready:9
- pionl/node-clone-ready:latest (node 9)

```docker
FROM pionl/node-clone-ready:8
```

## Cloning/accessing private repository

Add to your Dockerfile

```docker
# Get the private keys to enbale pull from private repo
ARG ssh_prv_key
RUN test -n "$ssh_prv_key"


# Authorize SSH Host
RUN mkdir -p /root/.ssh/ && \
    chmod 0700 /root/.ssh/

# Add the keys and set permissions
RUN echo "$ssh_prv_key" > /root/.ssh/id_rsa

RUN chmod 600 /root/.ssh/id_rsa
RUN chown -R root:root /root/.ssh

## Do your stuff that requires id_rsa
## Then delete the keys to prevent keeping it in the repo by calling

RUN rm -rf /root/.ssh/
```

Pass desired id_rsa file when building image:

```bash
docker build -t TAG_NAME --build-arg ssh_prv_key="$(cat ~/.ssh/id_rsa)"
```

## Contribution

1. Change the `Dockerfile.template`
2. Edit `build.sh` if new version is added
3. Run `build.sh` to build images
4. Run `build.sh deploy` to build and push images
