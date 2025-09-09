FROM codercom/enterprise-base:ubuntu

# Add uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/


USER root

ENV RUSTUP_HOME=/opt/rustup
ENV CARGO_HOME=/opt/cargo
ENV PATH=/opt/cargo/bin:$PATH

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path --profile minimal --default-toolchain nightly --default-host x86_64-unknown-linux-gnu && \
    chmod -R a+w ${RUSTUP_HOME} ${CARGO_HOME}

USER coder
