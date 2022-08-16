FROM nvidia/cuda:10.2-cudnn8-devel-ubuntu18.04
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
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends \
        python3.8 \
        python3-pip \
        python3-dev \
    && rm -rf /var/lib/apt/lists/*

RUN rm -f /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python
RUN rm -f /usr/bin/pip && ln -s /usr/bin/pip3 /usr/bin/pip

RUN pip --no-cache-dir install --upgrade setuptools
RUN pip --no-cache-dir install --upgrade torch===1.11.0 torchvision===0.12.0 torchaudio===0.11.0

RUN pip --no-cache-dir install --upgrade boto3 regex requests sacremoses sentencepiece tqdm
RUN pip --no-cache-dir install --upgrade datasets, transformers tensorboardX

RUN pip --no-cache-dir install --upgrade nltk
RUN python -m nltk.downloader all

RUN pip --no-cache-dir install --upgrade spacy
RUN python -m spacy download en

CMD ["/bin/bash"]