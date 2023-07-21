FROM rocm/dev-ubuntu-20.04:5.2.3
LABEL maintainer="Hugging Face"

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.9 \
    python3.9-dev \
    python3-pip \
    git \
    espeak-ng \
    ffmpeg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1 && \
    python -m pip install -U pip

ARG PYTORCH='1.13.1'
ARG ROCM='5.2'

RUN pip install --no-cache-dir torch==1.13.1+rocm5.2 torchvision==0.14.1+rocm5.2 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/rocm5.2 && \
    pip install --no-cache-dir git+https://github.com/facebookresearch/detectron2.git pytesseract

ARG REF="rocm-ci"
RUN git clone https://github.com/fxmarty/transformers && \
    cd transformers && \
    git checkout $REF && \
    pip install --no-cache-dir -e .[dev-torch]
