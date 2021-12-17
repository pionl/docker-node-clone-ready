FROM node:8

MAINTAINER Martin Kluska <martin@kluska.cz>

########################################################################################################################
##### Install ssh/git requirements
########################################################################################################################
RUN apt-get update && \
    apt-get install -y \
        git \
        openssh-server && rm -rf /var/lib/apt/lists/*
