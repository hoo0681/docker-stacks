# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=hoo0681
ARG BASE_CONTAINER=scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Install Tensorflow
RUN pip install --upgrade pip && \
    pip install --no-cache-dir "tensorflow-gpu" && \
    pip install --no-cache-dir keras

RUN mamba install --quiet --yes \
    pyyaml mkl mkl-include setuptools cmake cffi typing && \
    conda clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"  
RUN pip install  --no-cache-dir torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html

USER root

RUN apt install nvtop && \
    rm -rf /var/lib/apt/lists/*
    
RUN fix-permissions /home/$NB_USER

USER $NB_UID