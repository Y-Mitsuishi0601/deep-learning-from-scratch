# Deep Learning from Scratch - 開発環境

このリポジトリは、`uv` パッケージマネージャーと **Dev Containers** を使用した、Numpy および Matplotlib による数値計算・深層学習の演習環境です。

## 🚀 特徴

- **高速なパッケージ管理**: `uv` を使用し、コンテナ内での依存関係解決を高速化。
- **再現性**: Docker + Dev Containers により、どのマシンでも同じ環境が即座に立ち上がります。
- **ハイブリッド環境**: 演習用の Jupyter Notebook と、本番用の純粋な Python スクリプトの両方をサポート。
- **将来の拡張性**: FastAPI を追加して API サーバーとしてデプロイすることを想定した構成。

## 🛠 前提条件

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows/Mac) または Docker Engine (Linux)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- (Windows の場合) WSL2 環境推奨

## 📂 ディレクトリ構成

```text
deep-learning-from-scratch/
├── .devcontainer/
│   ├── devcontainer.json    # VS Code設定
│   ├── docker-compose.yml   # コンテナ構成
│   └── Dockerfile           # uvベースのイメージ定義
├── notebooks/               # .ipynb 演習用ファイル
├── src/                     # .py 本番用ソースコード
├── pyproject.toml           # 依存関係定義
└── README.md                # このファイル

```

## ⚡ セットアップ手順

1. **リポジトリを開く**
VS Code でこのフォルダ（`deep-learning-from-scratch`）を開きます。
2. **Dev Container を起動**
右下に表示されるポップアップの **"Reopen in Container"** をクリックします。
（表示されない場合は、`F1` キーを押し、`Dev Containers: Reopen in Container` を選択してください）
3. **ビルドの完了を待つ**
初回起動時は Docker イメージのビルドとパッケージの同期（`uv sync`）が自動で走ります。数分かかる場合があります。
4. **動作確認**
コンテナ内のターミナルで以下のコマンドを実行し、Numpy が正常に動作するか確認してください。
```bash
python -c "import numpy; print(f'Numpy version: {numpy.__version__}')"

```



## 📖 使い方

### Jupyter Notebook で演習する

1. `notebooks/` フォルダ内に `.ipynb` ファイルを作成します。
2. VS Code の右上のカーネル選択で `.venv/bin/python` が選択されていることを確認してください。

### Python スクリプトを実行する

`src/` 内のファイルは以下のコマンドで実行できます。

```bash
python src/main.py

```

### パッケージの追加

新しいライブラリ（例: `pandas`）を追加したい場合は、コンテナ内のターミナルで以下を実行します。

```bash
uv add pandas

```

## 🚀 将来の拡張 (FastAPI)

API サーバーとして起動する準備ができたら、以下のコマンドでライブラリを追加してください。

```bash
uv add fastapi uvicorn[standard]

```

その後、`src/main.py` に FastAPI のコードを記述し、ポート `8000` でアクセス可能になります。