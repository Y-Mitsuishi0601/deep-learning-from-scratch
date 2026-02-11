FROM python:3.12-slim-bookworm

# 1. uvのインストール
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 2. システム依存関係のインストール
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

# 3. 一般ユーザー 'vscode' を作成 (chownの前に実行)
RUN useradd -m -s /bin/bash vscode

# 4. 作業ディレクトリの設定と所有権の付与
WORKDIR /app
RUN chown vscode:vscode /app

# 5. 以降の操作を vscode ユーザーで行う
USER vscode

# 6. 依存関係の同期
# キャッシュマウントの uid を 1000 (vscodeユーザー) に指定
RUN --mount=type=cache,target=/home/vscode/.cache/uv,uid=1000 \
    --mount=type=bind,source=pyproject.toml,target=pyproject.toml \
    uv sync --no-install-project

# 7. 仮想環境のパスを優先的に使用
ENV PATH="/app/.venv/bin:$PATH"

CMD ["python3"]