FROM pytorch/pytorch:1.9.0-cuda11.1-cudnn8-runtime

#依存関係のインストール
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    git \
    cmake \
    build-essential \
    libturbojpeg0-dev

# Lite-HRNet リポジトリのクローン
WORKDIR /workspace
RUN git clone https://github.com/HRNet/Lite-HRNet.git

# COCOAPI のビルドとインストール
WORKDIR /workspace/Lite-HRNet/lib/cocoapi/PythonAPI
RUN python setup.py build_ext install

# 作業ディレクトリの設定
WORKDIR /workspace/Lite-HRNet

# 環境変数の設定
ENV PYTHONPATH "${PYTHONPATH}:/workspace/Lite-HRNet"

# 推論の実行コマンド
CMD ["python", "tools/test.py", "--cfg", "experiments/coco/hrnet/w32_256x192_adam_lr1e-3.yaml", "--modelDir", "pretrained/pose_coco/pose_hrnet_w32_256x192.pth"]