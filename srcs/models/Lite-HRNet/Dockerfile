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

RUN pip3 install \
tqdm \
pyyaml \
yacs \
opencv-python-headless \
scikit-image \
scikit-learn

RUN mkdir -p /workspace

WORKDIR /workspace
RUN git clone https://github.com/shmorish/skelton-pose-movement.git
RUN cp -r skelton-pose-movement/srcs/models/Lite-HRNet/ .
RUN rm -rf skelton-pose-movement

WORKDIR /workspace/Lite-HRNet
RUN pip3 install -r requirements.txt

RUN echo "export PS1='Docker Lite-HRNet:\w\$ '" >> ~/.bashrc