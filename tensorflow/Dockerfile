FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu20.04
LABEL author.name="Steve Zheng"
LABEL author.email="stevezheng23@gmail.com"

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
        software-properties-common \
    && rm -rf /var/lib/apt/lists/*

RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt-get update && apt-get install -y --no-install-recommends \
        python3.9 \
        python3.9-dev \
        python3.9-distutils \
    && rm -rf /var/lib/apt/lists/*

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python3.9 get-pip.py && rm get-pip.py

RUN rm -f /usr/bin/python3 && ln -s /usr/bin/python3.9 /usr/bin/python3
RUN rm -f /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python
RUN rm -f /usr/bin/pip && ln -s /usr/bin/pip3 /usr/bin/pip

RUN pip --no-cache-dir install --upgrade setuptools
RUN pip --no-cache-dir install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-2.9.0-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl

RUN pip --no-cache-dir install --upgrade sentencepiece tqdm

RUN pip --no-cache-dir install --upgrade spacy
RUN python -m spacy download en

CMD ["/bin/bash"]
