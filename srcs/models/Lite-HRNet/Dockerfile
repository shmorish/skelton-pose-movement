FROM ubuntu:20.04

RUN apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
git \
python3-pip \
ffmpeg \
libsm6 \
libxext6 \
curl \
unzip \
wget \
&& rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip

RUN pip3 install numpy \
opencv-python \
torch \
torchvision \
tqdm \
pyyaml \
yacs \
opencv-python-headless \
scipy \
scikit-image \
scikit-learn


RUN pip3 install mmcv-full==1.3.8 -f https://download.openmmlab.com/mmcv/dist/cu102/torch1.9.0/index.html

WORKDIR /workspace/Lite-HRNet
RUN pip3 install -r requirements.txt
