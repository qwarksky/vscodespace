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
##ENV NVIDIA_CONTAINER_TOOLKIT_VERSION=1.18.1-1

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
    gnupg2 \
    git \
    pipx \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libncurses5-dev \
    libncursesw5-dev\
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
    wget \
    llvm \
    python3-openssl \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /var/cache/apt/archives/* \
&& mkdir workspace \
&& mkdir -p workspace/sourcedata \
&& mkdir -p workspace/report \
&& mkdir -p workspace/export \
&& chsh -s $(which zsh) \
&& sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" \
&& curl -fsSL https://pyenv.run | bash \
&& curl -sSL https://install.python-poetry.org | POETRY_HOME=/etc/poetry python3 -


##RUN apt-get install -y nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
##    nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
##    libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
##    libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}
##RUN nvidia-ctk runtime configure --runtime=docker \
##&& systemctl restart docker

RUN echo "eval '$(pyenv init --path)' >> $HOME/.zshrc" \
&& echo "eval '$(pyenv init -)' >> $HOME/.zshrc" \
&& echo "eval '$(pyenv virtualenv-init -)' >> $HOME/.zshrc" \
&& pyenv install 3.13 \
&& pyenv local 3.13

COPY pyproject.toml ../workspace
WORKDIR /workspace
RUN uv sync
VOLUME /workspace/sourcedata
VOLUME /workspace/report
VOLUME /workspace/export


