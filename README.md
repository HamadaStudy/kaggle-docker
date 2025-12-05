# 概要
Kaggle Notebook環境をローカルに構築する

# 手順
## 1. 作業ディレクトリの作成
```shell
$ git clone hoge {kaggle} # 作業ディレクトリを作成
$ cd {kaggle}
```

## 2. ファイルの修正

### 2.1 CUDAドライバのバージョンを確認
```powershell
# powershellでバージョン確認
PS C:\\Users\\user> nvidia-smi
Wed Dec  3 22:36:56 2025
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 581.80                 Driver Version: 581.80         CUDA Version: 13.0     | # versionは13.0
+-----------------------------------------+------------------------+----------------------+
# ...
```

### 2.2 対応するPytorchのバージョンを確認し、`Dockerfile`を編集
[text](https://pytorch.org/)
```docker
# ...
RUN pip install torch torchvision --index-url https://download.pytorch.org/whl/cu130
# ...
```

### 2.3 環境変数の設定
Kaggle API Tokenなどの環境変数を`.env`ファイルへ記入
```
KAGGLE_API_TOKEN = {API Key}
```

## 3. DevContainerの起動
```shell
$ code .
``` 
コンテナで開くを選択

`notebook/MNIST_tutorial.ipynb`を実行できたらOK

# Tips
## おすすめディレクトリ構成
```
========================
WSL側
------------------------

/kaggle/ <- マウント
  │
  ├─README.md
  │
  ├─.devcontainer/ <- イメージの切り替えはこの中のファイルを編集することで対応
  │
  ├─sample/
  │  │
  │  ├─dataset
  │  │
  │  └─sample_notebook.ipynb
  │
  ├─competitionA
  │
  ├─competitionB
  │
  └─input/	
    │
    ├─competionA
    │
    └─competionB

========================
Docker側
------------------------

/kaggle/ <- マウント
	│
	├─competitionA
	│
	├─competitionB
	│
	└─input/	
		│
		├─competionA
		│
		└─competionB
```

## VSCode拡張機能
デフォルトで入っている拡張機能一覧
```
====================================================
VS Code 拡張機能リストと役割の概要
====================================================

"extensions": [
  // データ分析・視認性
  "mechatroner.rainbow-csv",        // CSVファイルを列ごとに色分けして表示

  // Python コード整形・標準化
  "ms-python.black-formatter",      // PythonコードをBlack規約で自動整形
  "ms-python.isort",                // Pythonのインポート文を自動ソート

  // AI/Claude 関連
  "andrepimenta.claude-code-chat",  // Claude Code Chatの非公式UI (要確認)
  "anthropic.claude-code",          // Anthropic公式のClaude Codeサポート

  // 言語パック
  "ms-ceintl.vscode-language-pack-ja", // VS Codeの日本語化

  // Python開発環境コア機能
  "ms-python.debugpy",              // Pythonコードのデバッグ機能
  "ms-python.python",               // 基本的なPython言語サポート
  "ms-python.vscode-python-envs",   // Python仮想環境の管理・検出

  // Jupyter/データサイエンス関連
  "ms-toolsai.jupyter",             // Jupyter Notebookの基本的なサポート
  "ms-toolsai.jupyter-keymap",      // Jupyterセル操作用のショートカットキー
  "ms-toolsai.jupyter-renderers",   // Jupyterの出力レンダリング
  "ms-toolsai.vscode-jupyter-cell-tags", // Jupyterセルのタグ付け
  "ms-toolsai.vscode-jupyter-slideshow"  // Jupyterスライドショー表示機能
]
```
