# Docker image based on official node image with openssh and git installed

## Pre-installed packages:

- git and openssh-server for cloning support

## Tags:

![](https://img.shields.io/docker/pulls/pionl/node-clone-ready?style=flat-square) ![](https://img.shields.io/docker/stars/pionl/node-clone-ready?style=flat-square)

Image | Badges
 --- | ---
**pionl/node-clone-ready:8** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/8?style=flat-square)
**pionl/node-clone-ready:9** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/9?style=flat-square)
**pionl/node-clone-ready:12** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/12?style=flat-square)
**pionl/node-clone-ready:14** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/14?style=flat-square)
**pionl/node-clone-ready:16** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/16?style=flat-square)
**pionl/node-clone-ready:17** | ![](https://img.shields.io/docker/image-size/pionl/node-clone-ready/17?style=flat-square)


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

## Contributions

1. Install [wf-docker](https://github.com/wrk-flow/wf-docker)
2. Change the `Dockerfile.template`
3. For new versions edit `.wf-docker.json` and `wf-docker.tags` property
4. Use `wf-docker build` to build image

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
