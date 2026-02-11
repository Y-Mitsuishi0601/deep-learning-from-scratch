FROM mcr.microsoft.com/vscode/devcontainers/python:3.12

# 1. uvのインストール
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 2. システム依存関係のインストール
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql-client \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

ENV UV_PROJECT_ENVIRONMENT=/app/.venv \
    PYTHONUNBUFFERED=1 \
    UV_LINK_MODE=copy

# 4. 作業ディレクトリの設定と所有権の付与
WORKDIR /app