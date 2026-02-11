FROM python:3.12-slim-bookworm

# uvのインストール
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# システムの依存関係（matplotlibの描画などに必要な場合がある）
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# 依存関係のコピーとインストール
# キャッシュを効率化するため、まず設定ファイルだけコピー
RUN --mount=type=cache,target=/root/.cache/uv \
    --mount=type=bind,source=pyproject.toml,target=pyproject.toml \
    --mount=type=bind,source=uv.lock,target=uv.lock \
    uv sync --frozen --no-install-project

# 環境変数の設定（uvが作成した仮想環境を優先的に使用）
ENV PATH="/app/.venv/bin:$PATH"

# デフォルトのコマンド（Dev Containerで上書きされるが、単体起動用）
CMD ["python3"]