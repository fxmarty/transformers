FROM rocm/dev-ubuntu-20.04:5.2.3
LABEL maintainer="Hugging Face"

ARG DEBIAN_FRONTEND=noninteractive

# The following `ARG` are mainly used to specify the versions explicitly & directly in this docker file, and not meant
# to be used as arguments for docker build (so far).

ARG PYTORCH='1.13.1'
# (not always a valid torch version)
ARG INTEL_TORCH_EXT='1.11.0'
# Example: `cu102`, `cu113`, etc.
ARG ROCM='5.2'
ARG TENSORFLOW='2.12.0.560'

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

RUN pip install --no-cache-dir torch==$PYTORCH+rocm$ROCM torchvision==0.14.1+rocm$ROCM torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/rocm$ROCM && \
    pip install --no-cache-dir git+https://github.com/facebookresearch/detectron2.git pytesseract && \
    pip install --no-cache-dir tensorflow-rocm==$TENSORFLOW

ARG REF="rocm-ci"
RUN git clone https://github.com/fxmarty/transformers && \
    cd transformers && \
    git checkout $REF && \
    pip install --no-cache-dir -e .[dev-rocm]

RUN python3 -m pip install --no-cache-dir git+https://github.com/huggingface/accelerate@main#egg=accelerate

# For bettertransformer
RUN python3 -m pip install --no-cache-dir optimum

# For video model testing
RUN python3 -m pip install --no-cache-dir decord av==9.2.0

# For `dinat` model
RUN python3 -m pip install --no-cache-dir natten -f https://shi-labs.com/natten/wheels/$CUDA/
