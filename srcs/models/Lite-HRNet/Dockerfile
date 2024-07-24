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

RUN curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg   && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list |     sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' |     tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
RUN sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list
RUN apt-get update
RUN apt-get install -y --no-install-recommends nvidia-container-toolkit
RUN sed -i 's/^#no-cgroups = false/no-cgroups = false/' /etc/nvidia-container-runtime/config.toml

RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends nvidia-driver-515