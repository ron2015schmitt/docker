
#  Ubuntu, curl, NVM, NodeJS,


FROM ubuntu:22.04
RUN echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/00-docker
RUN echo 'APT::Install-Recommends "0";' >> /etc/apt/apt.conf.d/00-docker
SHELL ["/bin/bash", "-c"]

# NODE_VERSION=18.18 comes with npm 9.8.1 and corepack 0.19.0
ENV NODE_VERSION=18.18.0  
ENV NPM_VERSION=10.2.0
ENV NVM_VERSION=0.39.5
ENV PNPM_VERSION=8.8.0
ENV ANGULAR_VERSION=16.2.5
ENV VITE_VERSION=4.4.11

# Expose ports
# 4200 is default used by Angular
# 4200 is default used by Vite
EXPOSE 4200  
EXPOSE 5173

# Install curl 
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update && \
  apt-get upgrade -y &&\
  apt-get install -y ca-certificates curl dos2unix git vim


RUN chmod a+rx /root/.bashrc

# create user account
RUN useradd -ms /bin/bash user
USER user
ENV HOME=/home/user
WORKDIR ${HOME}
RUN echo "HOME=${HOME}"

# copy content of aliases into the .bashrc file
COPY aliases ${HOME}/temp
RUN dos2unix --allow-chown ${HOME}/temp
RUN cat temp >> ${HOME}/.bashrc && rm temp


# Install NVM via curl
# https://github.com/nvm-sh/nvm#installing-and-updating
# by default it installs to ~/.nvm
#ENV XDG_CONFIG_HOME=${HOME}
ENV NVM_DIR=${HOME}/.nvm
RUN mkdir ${NVM_DIR}
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v${NVM_VERSION}/install.sh | bash

# Install NodeJS via nvm
RUN source ${NVM_DIR}/nvm.sh && \
  nvm install ${NODE_VERSION} && \
  nvm use v${NODE_VERSION} && \
  nvm alias default v${NODE_VERSION} && \
  nvm install --latest-npm


# Install npm via npm
RUN source ${NVM_DIR}/nvm.sh && \
  npm install -g npm@~${NPM_VERSION}

# Install PNPM via corepack
RUN source ${NVM_DIR}/nvm.sh &&\
  corepack enable && corepack prepare pnpm@${PNPM_VERSION} --activate && SHELL=${SHELL} pnpm setup

# Enable `pnpm add --global` on Alpine Linux by setting
# home location environment variable to a location already in $PATH
# https://github.com/pnpm/pnpm/issues/784#issuecomment-1518582235
ENV PNPM_HOME=/usr/local/bin
ENV PATH="${PATH}:${PNPM_HOME}"
USER root

#Install Angular via pnpm
RUN source ${NVM_DIR}/nvm.sh && pnpm add --global @angular/cli@${ANGULAR_VERSION}



