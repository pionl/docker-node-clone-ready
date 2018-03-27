# Docker image based on official node image with openssh and git installed

## Pre-installed packages:

- git and openssh-server for cloning support

## Tags:

- pionl/node-clone-ready:8
- pionl/node-clone-ready:9
- pionl/node-clone-ready:lastest (node 9)

```docker
FROM pionl/node-clone-ready:8
```

## Contribution

1. Change the `Dockerfile.template`
2. Edit `build.sh` if new version is added
3. Run `build.sh` to build images
4. Run `build.sh deploy` to build and push images
