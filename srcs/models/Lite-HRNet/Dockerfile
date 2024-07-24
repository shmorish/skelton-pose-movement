FROM nvidia/cuda:11.8.0-base-ubuntu20.04

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3-pip
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends python3.9
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 1
RUN update-alternatives --config python3

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends git
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends ffmpeg
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libsm6
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libxext6
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends curl
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends unzip
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends wget
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends vim

RUN pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
RUN rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip

RUN pip3 install \
tqdm \
pyyaml \
yacs \
opencv-python-headless \
scikit-image \
scikit-learn \
ninja

RUN mkdir -p /workspace

WORKDIR /workspace
RUN git clone https://github.com/shmorish/skelton-pose-movement.git
RUN cp -r skelton-pose-movement/srcs/models/Lite-HRNet/ .
RUN rm -rf skelton-pose-movement

WORKDIR /workspace/Lite-HRNet
RUN pip3 install -r requirements.txt

RUN pip install -U openmim
# RUN mim install mmcv==2.0.0

RUN echo "export PS1='Docker Lite-HRNet:\w\$ '" >> ~/.bashrc

# python3 tools/test.py configs/top_down/lite_hrnet/coco/litehrnet_18_coco_256x192.py
# CMD