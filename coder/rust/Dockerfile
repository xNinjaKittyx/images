
FROM codercom/enterprise-base:ubuntu

# NOTE: This is no longer just rust. It's basically just my dev env at this point. Maybe I'll make smaller builds, but I don't have a need right now.


# Add uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/


USER root

ENV RUSTUP_HOME=/opt/rustup
ENV CARGO_HOME=/opt/cargo
ENV PATH=/opt/cargo/bin:$PATH

# Packages needed based on using rust-discord-bot project.
RUN apt update && apt install -y pkg-config cmake libssl-dev gpg-agent

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path --profile minimal --default-toolchain nightly --default-host x86_64-unknown-linux-gnu && \
    chmod -R a+w ${RUSTUP_HOME} ${CARGO_HOME}

# Adding DotNet 9.0 for Jellyfin Plugins
RUN sudo add-apt-repository ppa:dotnet/backports && \
    sudo apt-get update && \
    sudo apt-get install -y dotnet-sdk-9.0

# TODO: Remove when this issue is fixed: https://github.com/nestybox/sysbox/issues/973 
# Temporarly fix containerd version 
# RUN sudo apt-get install -y --allow-downgrades "containerd.io=1.7.28-1~ubuntu.24.04~noble" && sudo apt-mark hold containerd.io
# ARG DOCKER_VERSION=5:28.5.1-1~ubuntu.24.04~noble

# RUN apt-get install -y --no-install-recommends --allow-downgrades \
#      docker-ce=${DOCKER_VERSION} \
#      docker-ce-cli=${DOCKER_VERSION} \
#      containerd.io \
#      docker-buildx-plugin \
#      docker-compose-plugin \
#   && apt-mark hold docker-ce docker-ce-cli containerd.io \
#   && rm -rf /var/lib/apt/lists/*

# Install BunJS
RUN curl -fsSL https://bun.sh/install | bash

# Install Codex
RUN ~/.bun/bin/bun install -g @openai/codex

# Install claude-cli
RUN curl -fsSL https://claude.ai/install.sh | bash

RUN sudo add-apt-repository ppa:zhangsongcui3371/fastfetch && \
    sudo apt-get update && \
    sudo apt-get install -y fastfetch

RUN rustup component add rustfmt && cargo install just

RUN rm -rf /var/lib/apt/lists/*
    

USER coder
