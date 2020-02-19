FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04
MAINTAINER Steve Zheng "stevezheng23@gmail.com"

# set debian frontend as non-interactive
ENV DEBIAN_FRONTEND=noninteractive

# ensure local python is preferred over distribution python
ENV PATH /usr/local/bin:$PATH

RUN apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        wget \
        vim \
        git \
        openssh-client \
        gcc g++ \
        zip unzip \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends \
        python3.6 \
        python3-pip \
        python3-dev \
    && rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/python3 /usr/bin/python & \
    ln -s /usr/bin/pip3 /usr/bin/pip

RUN pip --no-cache-dir install --upgrade setuptools
RUN pip --no-cache-dir install --upgrade torch===1.4.0 torchvision===0.5.0 -f https://download.pytorch.org/whl/torch_stable.html

RUN pip --no-cache-dir install --upgrade boto3 regex requests sacremoses sentencepiece tqdm
RUN pip --no-cache-dir install --upgrade transformers tensorboardX

RUN pip --no-cache-dir install --upgrade spacy
RUN python -m spacy download en

WORKDIR /tmp/nvidia_apex
RUN git clone https://github.com/NVIDIA/apex.git
WORKDIR /tmp/nvidia_apex/apex
RUN pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .
WORKDIR /
RUN rm -r /tmp/

CMD ["/bin/bash"]