# Deep Learning from Scratch - 開発環境

このリポジトリは、`uv` パッケージマネージャーと **Dev Containers** を使用した、Numpy および Matplotlib による数値計算・深層学習の演習環境です。

## 🚀 特徴

- **高速なパッケージ管理**: `uv` を使用し、コンテナ内での依存関係解決を高速化。
- **再現性**: Docker + Dev Containers により、どのマシンでも同じ環境が即座に立ち上がります。
- **JupyterLab 自動起動**: Dev Container 起動時に JupyterLab が自動的にバックグラウンドで起動します。
- **ハイブリッド環境**: 演習用の JupyterLab と、本番用の純粋な Python スクリプトの両方をサポート。
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
│   ├── devcontainer.json    # VS Code設定（JupyterLab自動起動含む）
│   ├── docker-compose.yml   # コンテナ構成
│   └── Dockerfile           # uvベースのイメージ定義
├── notebooks/               # .ipynb 演習用ファイル
├── data/                    # データセット保存用
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
完了後、JupyterLab が自動的にバックグラウンドで起動します（ポート 8888）。
4. **動作確認**
   - JupyterLab: ブラウザで `http://localhost:8888` にアクセス
   - Python: コンテナ内のターミナルで以下のコマンドを実行
   ```bash
   python -c "import numpy; print(f'Numpy version: {numpy.__version__}')"
   ```



## 📖 使い方

### JupyterLab で演習する

Dev Container 起動時に JupyterLab が自動的に起動します（ポート 8888）。

1. **JupyterLab にアクセス**
   - VS Code 内に表示される通知から「ブラウザで開く」をクリック
   - または、ブラウザで `http://localhost:8888` にアクセス
   - トークン認証は無効化されているため、そのままアクセスできます

2. **ノートブックの操作**
   - `notebooks/` フォルダ内に `.ipynb` ファイルを作成
   - JupyterLab または VS Code のノートブックエディタで編集可能

3. **JupyterLab の再起動**
   コンテナ内のターミナルで以下を実行:
   ```bash
   pkill -f jupyter  # 停止
   jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='' &  # 再起動
   ```

### VS Code で Jupyter Notebook を使う

JupyterLab の代わりに VS Code のノートブックエディタも使用できます:

1. `notebooks/` フォルダ内に `.ipynb` ファイルを作成します。
2. VS Code の右上のカーネル選択で `.venv/bin/python` が選択されていることを確認してください。

### Python スクリプトを実行する（オプション）

通常の Python ファイル（`.py`）を実行する場合:

```bash
python your_script.py
```

### パッケージの追加

新しいライブラリ（例: `pandas`）を追加したい場合は、コンテナ内のターミナルで以下を実行します。

```bash
uv add pandas

```

## 🚀 将来の拡張 (FastAPI)

API サーバーとして起動する準備ができたら、以下のコマンドでライブラリを追加してください。

```bash
uv sync --extra api
```

その後、Python ファイルに FastAPI のコードを記述し、ポート `8000` でアクセス可能になります。