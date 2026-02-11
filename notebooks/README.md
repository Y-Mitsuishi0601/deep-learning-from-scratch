# JupyterLab Notebook環境について

このディレクトリには、JupyterLab Notebook環境で使用するノートブックファイルが含まれています。ノートブックは、データ分析、機械学習、可視化などのタスクに便利なインタラクティブなドキュメント形式です。

## Notebookをブラウザで開く

```bash
# JupyterLabを起動
uv run jupyter lab --notebook-dir=/app --no-browser --ip=0.0.0.0 --port=8888 --ServerApp.token=''
```

上記のコマンドを実行すると、JupyterLabが起動し、ブラウザでアクセスできるようになります。ブラウザで[このURL](http://127.0.0.1:8888/lab/)にアクセスしてください。

## 備考

本プロジェクトでは、`.ipynb`拡張子を持つファイルはGithub上で管理されません。
