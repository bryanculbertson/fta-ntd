# See here for image contents: https://github.com/devcontainers/images/tree/main/src/base-ubuntu

# [Choice] Ubuntu version: noble
ARG VARIANT="noble"
FROM mcr.microsoft.com/vscode/devcontainers/base:2-${VARIANT}

# Install system dependancies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        bash \
        build-essential \
        curl \
        expat \
        fontconfig \
        gcc \
        git \
        libbz2-dev \
        libffi-dev \
        liblzma-dev \
        libmpfr-dev \
        libncurses-dev \
        libpq-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        libxml2-dev \
        libxmlsec1-dev \
        llvm \
        locales \
        make \
        openssl \
        pipx \
        python3-dev \
        python3-pip \
        sudo \
        tk-dev \
        unzip \
        vim \
        wget \
        wget \
        xz-utils \
        zip \
        zlib1g \
        zlib1g-dev \
        zsh \
    && apt-get clean

# Install project dependancies
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        shellcheck \
    && apt-get clean

# Set the locale
RUN locale-gen --no-purge en_US.UTF-8
ENV LANG=en_US.UTF-8 \ LANGUAGE=en_US:en \ LC_ALL=en_US.UTF-8

# Set user to non-root
USER 1000:1000
ENV HOME /home/vscode

# Install pyenv
ENV PYENV_ROOT="${HOME}/.pyenv"
RUN curl https://pyenv.run/ | /bin/bash
ENV PATH="$PYENV_ROOT/bin:${PATH}"

RUN echo '' >> $HOME/.bashrc \
    && echo 'export PYENV_ROOT="$HOME/.pyenv"' >> $HOME/.bashrc \
    && echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> $HOME/.bashrc \
    && echo 'eval "$(pyenv init -)"' >> $HOME/.bashrc \
    && echo 'eval "$(pyenv virtualenv-init -)"' >> $HOME/.bashrc

# Install Python
ARG PYTHON_VERSION=3.13.5
RUN eval "$(pyenv init --path)" \
    && pyenv install ${PYTHON_VERSION}

# Install Poetry
ARG POETRY_VERSION=2.1.3
RUN pipx ensurepath \
    && pipx install poetry==${POETRY_VERSION}
