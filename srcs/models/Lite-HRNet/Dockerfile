FROM nvidia/cuda:11.3.1-devel-ubuntu20.04

WORKDIR /workspace

COPY ./requirements.txt ./requirement/requirements.txt
COPY ./requirements/ ./requirement/requirements

RUN apt-get update && apt-get install -y \
    python3-pip \
    git \
    wget \
    vim \
    zip \
    unzip \
    curl \
    libgl1-mesa-glx libglib2.0-0\
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir --upgrade pip
RUN pip3 install torch==1.12.1+cu113 torchvision==0.13.1+cu113 torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113
RUN pip3 install --no-cache-dir -r ./requirement/requirements.txt
RUN pip3 install mmcv==1.6.0 -f https://download.openmmlab.com/mmcv/dist/cu113/torch1.12/index.html
RUN pip3 install mmpose==0.25.1
RUN pip3 install yapf==0.40.1
RUN pip3 install mmengine
RUN pip3 install opencv-python

# makeing the directory for the model
RUN mkdir -p /workspace/Lite-HRNet/data/coco/
# RUN mkdir -p /workspace/Lite-HRNet/data/coco/anotations
# RUN mkdir -p /workspace/Lite-HRNet/data/coco/person_detection_results
# RUN mkdir -p /workspace/Lite-HRNet/data/coco/train2017
# RUN mkdir -p /workspace/Lite-HRNet/data/coco/val2017

WORKDIR /workspace/Lite-HRNet/data/coco

# Download the COCO dataset
RUN wget http://images.cocodataset.org/annotations/annotations_trainval2017.zip
RUN unzip annotations_trainval2017.zip
RUN rm annotations_trainval2017.zip

# Download the COCO dataset
RUN wget http://images.cocodataset.org/zips/train2017.zip
RUN unzip train2017.zip
RUN rm train2017.zip

# Download the COCO dataset
RUN wget http://images.cocodataset.org/zips/val2017.zip
RUN unzip val2017.zip
RUN rm val2017.zip

# person detection results
# RUN wget https://download.openmmlab.com/mmpose/data/coco/person_detection_results.zip


WORKDIR /workspace/Lite-HRNet/data/coco/annotations
RUN rm captions_train2017.json captions_val2017.json instances_train2017.json instances_val2017.json 

# # RUN mkdir -p /workspace/Lite-HRNet/data/coco/person_detection_results
# # WORKDIR /workspace/Lite-HRNet/data/coco/person_detection_results
# RUN wget https://ffm9yw-ch3301.files.1drv.com/y4mME3XoqIXMaDII-DO8v7sps-FExrPi2vxphVlCcdEr7BNC3ckOz5kayj84jTmaoPBQuNVCYXa19OOAVfsbMj67gvgkxjLbRWkCAKs3lY-5UM8t6PaX-HjPKQK2pQmHeg1EQ5BJKS0XsUqpazhEtU9nmjVpr81nXI_HRzgb7KIVUhqD_LsCWDxinuNu-L3XyG8EPJYW3haahYmYfmB4EUerw