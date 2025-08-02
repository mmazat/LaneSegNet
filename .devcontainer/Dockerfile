FROM nvidia/cuda:11.6.1-devel-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive

# Install basic dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    git \
    wget \
    curl \
    ca-certificates \
    libopencv-dev \
    python3-dev \
    python3-pip \
    python3-setuptools \
    && rm -rf /var/lib/apt/lists/*

RUN pip install torch==1.9.1+cu111 torchvision==0.10.1+cu111 -f https://download.pytorch.org/whl/torch_stable.html

RUN pip install mmcv-full==1.5.2 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.9.0/index.html
RUN pip install mmdet==2.26.0
RUN pip install mmsegmentation==0.29.1
RUN pip install mmdet3d==1.0.0rc6

COPY requirements.txt .
RUN pip install -r requirements.txt

# Create a working directory
WORKDIR /workspace

# Set environment variables
ENV PYTHONPATH=/workspace:$PYTHONPATH
ENV PATH=/workspace/bin:$PATH

# Set the default command
CMD ["/bin/bash"]