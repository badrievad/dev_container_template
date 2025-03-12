# Используем базовый образ
FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

# Устанавливаем curl, git и zsh
RUN apt-get update && apt-get install -y \
    curl \
    git \
    zsh \
    && rm -rf /var/lib/apt/lists/*

# Переключаемся на пользователя vscode и устанавливаем oh‑my‑zsh вместе с плагинами и темой
USER vscode
WORKDIR /home/vscode

# Устанавливаем UV
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && \
    export PATH="$HOME/.local/bin:$PATH" && \
    uv self update

# Устанавливаем плагины для Zsh
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions && \
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# Устанавливаем тему spaceship
RUN git clone https://github.com/spaceship-prompt/spaceship-prompt.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship-prompt --depth=1 && \
    ln -s ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship-prompt/spaceship.zsh-theme ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/spaceship.zsh-theme

# Копируем кастомный .zshrc, если он у вас есть
COPY .zshrc /home/vscode/.zshrc

# Делаем Zsh оболочкой по умолчанию
SHELL ["/usr/bin/zsh", "-c"]

