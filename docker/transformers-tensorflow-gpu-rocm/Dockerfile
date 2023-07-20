FROM rocm/dev-ubuntu-20.04:5.2.3
LABEL maintainer="Hugging Face"

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.9 \
    python3.9-dev \
    python3-pip \
    git \
    espeak-ng \
    ffmpeg \
    rocm-libs \
    rccl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1 && \
    python -m pip install -U pip

ARG TENSORFLOW='2.12.0.560'

ADD "https://www.random.org/cgi-bin/randbyte?nbytes=10&format=h" skipcache
RUN pip install --no-cache-dir tensorflow-rocm==2.12.0.560

#ARG REF="rocm-ci"
#RUN git clone https://github.com/fxmarty/transformers && \
#    cd transformers && \
#    git checkout $REF && \
#    pip install --no-cache-dir -e .[dev-tensorflow-rocm]
