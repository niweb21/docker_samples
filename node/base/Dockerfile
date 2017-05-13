FROM ubuntu:16.04

ENV LANG C.UTF-8
ENV LANGUAGE C:en
ENV LC_ALL C.UTF-8

# Install packages
RUN apt-get update \
    && apt-get install -y \
        git \
        wget \
        xz-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add user node with home
RUN groupadd --gid 1000 node \
&& useradd --uid 1000 --gid node --shell /bin/bash --create-home node

# Install Node.js and npm
ENV NODE_VERSION 7.10.0

RUN wget -O /tmp/node https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz

RUN mkdir /opt/nodejs
RUN tar -xf /tmp/node -C /opt/nodejs
RUN ln -s /opt/nodejs/node-v$NODE_VERSION-linux-x64 /opt/nodejs/current

RUN ln -s /opt/nodejs/current/bin/node /bin/node
RUN ln -s /opt/nodejs/current/bin/npm /bin/npm

ENV PATH="/opt/nodejs/current/bin:${PATH}"

# Update npm, actually there is a bug with npm and docker
# RUN npm install npm@latest -g

# Install npm packages globally without sudo : https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md
RUN mkdir /home/node/.npm-packages
RUN echo 'prefix=/home/node/.npm-packages' > /home/node/.npmrc
RUN chown node:node /home/node/.npm-packages /home/node/.npmrc

RUN echo 'export NPM_PACKAGES="/home/node/.npm-packages"' >> /home/node/.bashrc
RUN echo 'export NODE_PATH="$NPM_PACKAGES/lib/node_modules${NODE_PATH:+:$NODE_PATH}"' >> /home/node/.bashrc
RUN echo 'export PATH="$NPM_PACKAGES/bin:$PATH"' >> /home/node/.bashrc
RUN echo 'export MANPATH="$NPM_PACKAGES/share/man"' >> /home/node/.bashrc
