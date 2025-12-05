# Dockerイメージの指定
FROM gcr.io/kaggle-gpu-images/python:v163

# 作業ディレクトリを設定
WORKDIR /kaggle

# 各々のGPUに対応するpytorchをインストール
RUN pip install torch torchvision --index-url https://download.pytorch.org/whl/cu130
ADD requirements.txt /kaggle/requirements.txt
RUN pip install -r requirements.txt

RUN curl -fsSL https://claude.ai/install.sh | bash

# jupyter notebookの起動
CMD ["jupyter", \
     "notebook", \
     "--ip=0.0.0.0", \
     "--allow-root", \
     "--no-browser", \
     "--NotebookApp.token=\"kaggle\"", \
     "--notebook-dir=/kaggle"]