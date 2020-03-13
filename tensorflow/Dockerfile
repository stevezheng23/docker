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

RUN rm -f /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python
RUN rm -f /usr/bin/pip && ln -s /usr/bin/pip3 /usr/bin/pip

RUN pip --no-cache-dir install --upgrade setuptools
RUN pip --no-cache-dir install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.13.1-cp36-cp36m-linux_x86_64.whl

RUN pip --no-cache-dir install --upgrade sentencepiece tqdm

RUN pip --no-cache-dir install --upgrade spacy
RUN python -m spacy download en

CMD ["/bin/bash"]
