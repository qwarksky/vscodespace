FROM ghcr.io/astral-sh/uv:trixie-slim
## https://docs.astral.sh/uv/guides/integration/docker/#available-images

LABEL maintainer="Ezio Qwarksky"


ENV HOME=/root
ENV PYENV_ROOT=$HOME/.pyenv
ENV PATH="$PYENV_ROOT/shims:$PYENV_ROOT/bin:$HOME/.local/bin:$PATH"

ENV UV_PROJECT_ENVIRONMENT=/workspace/.venv
ENV PATH="${UV_PROJECT_ENVIRONMENT}/bin:$PATH"
ENV UV_SYSTEM_PYTHON=1
ENV PATH="/workspace/.venv/bin:$PATH"
ENV PATH="/etc/poetry/bin:$PATH"

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN apt-get update && apt-get install -y --no-install-recommends \ 
    vim \
    neovim \
    nano \
    man \
    zsh \
    tmux \
    bat \
    curl \
    git \
    pipx \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /var/cache/apt/archives/* \
&& chsh -s $(which zsh) \
&& sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" \
&& curl -fsSL https://pyenv.run | bash \
&& curl -sSL https://install.python-poetry.org | POETRY_HOME=/etc/poetry python3 - \
&& mkdir workspace

COPY pyproject.toml ../workspace
WORKDIR workspace
RUN uv sync

## EXPOSE 8080

## Create a non-root user and switch to it
## https://docs.marimo.io/guides/deploying/deploying_docker/#prerequisites
## RUN useradd -m app_user
## USER app_user

## CMD ["marimo", "edit", "--no-token", "-p", "8080", "--host", "0.0.0.0"]
