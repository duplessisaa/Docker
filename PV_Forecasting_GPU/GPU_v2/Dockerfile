# Author and Source: https://github.com/ufoym/deepo/blob/master/docker/Dockerfile.all-jupyter-py36-cu90 
#
# Edited by: Armand du Plessis
# ------------------------------------------------------------------------------
# Based on the deep learning Docker images from https://github.com/ufoym/deepo.
# Usage with nvidia-docker:
#   $ nvidia-docker run -it --name my_container <image-build>:<tag>
# ------------------------------------------------------------------------------
# ==================================================================
# module list
# ------------------------------------------------------------------
#
# python        3.6    (apt)
# jupyter       latest (pip)
# tensorflow    1.12.0 (pip)
# keras         latest (pip)
# lasagne       latest (git)
# opencv        4.0.1  (git)
# sonnet        latest (pip)
# caffe         latest (git)
# cntk          latest (pip)
# ==================================================================
#
FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
#
# ==============================================================================
# Volume
# ------------------------------------------------------------------------------
#
#make a new directory notebooks used as container's volume 
RUN mkdir /notebooks
#
# Setting up volumes
VOLUME ["/notebooks"]
#
# Setup with docker as bind mount volume add the following to docker command:
# $ docker run -it --name <my_container_name> -v </path>:</notebooks> <image_name>:<image_tag>
#
# ------------------------------------------------------------------------------
# Ports Exposed
# ------------------------------------------------------------------------------	
#Ports exposed for Jupyter and tensorflow
EXPOSE 8889 6006
#
# Setup with docker the exposed ports to link container and the local machine's data volume
# by adding the following
# $ docker run -it --name <my_container_name> -v </path>:</notebooks> -p <local_machine_port>:8889 <image_name>:<image_tag>
#
# ==============================================================================
# Install all dependencies
# ------------------------------------------------------------------------------
#
#
RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \
#
    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \
#
    apt-get update && \
#
# ==================================================================
# tools
# ------------------------------------------------------------------
#
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        build-essential \
        ca-certificates \
        cmake \
        wget \
        git \
        vim \
        && \
#
#
# ==================================================================
# python
# ------------------------------------------------------------------
#
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        software-properties-common \
        && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        python3.6 \
        python3.6-dev \
        && \
    wget -O ~/get-pip.py \
        https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ~/get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    $PIP_INSTALL \
        setuptools==40.8.0 \
        pip==19.1.1 \
        && \
    $PIP_INSTALL \	
        numpy \
        scipy \
	seaborn==0.9.0 \
        pandas==0.24.1\
	pandas-profiling \
	pvlib==0.6.0 \
        cloudpickle \
	pickleshare \
        scikit-learn==0.20.0 \
	python-dateutil==2.7.5 \
        matplotlib \
	PyMySQL==0.9.2 \
	mkl-fft \
	mkl-random \
	windrose==1.6.5 \
        Cython \
	tables==3.4.4 \
        && \		

# ==================================================================
# jupyter
# ------------------------------------------------------------------
#
# Run Jupyter from inside the container with
# $ jupyter notebook --ip=0.0.0.0 --no-browser --port=8889 --allow-root
#
    $PIP_INSTALL \
        jupyter \
        && \
#
#
#
# ==================================================================
# tensorflow
# ------------------------------------------------------------------
#
    $PIP_INSTALL \
        tensorflow-gpu==1.12.0\
        && \
#
#
# ==================================================================
# keras
# ------------------------------------------------------------------
#
    $PIP_INSTALL \
        h5py \
        keras \
        && \
# 
# ==================================================================
# opencv
# ------------------------------------------------------------------
#
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        libatlas-base-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        && \
#
    $GIT_CLONE --branch 4.0.1 https://github.com/opencv/opencv ~/opencv && \
    mkdir -p ~/opencv/build && cd ~/opencv/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_IPP=OFF \
          -D WITH_CUDA=OFF \
          -D WITH_OPENCL=OFF \
          -D BUILD_TESTS=OFF \
          -D BUILD_PERF_TESTS=OFF \
          .. && \
    make -j"$(nproc)" install && \
    ln -s /usr/local/include/opencv4/opencv2 /usr/local/include/opencv2 && \
# 
# 
# ==================================================================
# config & cleanup
# ------------------------------------------------------------------
#
    ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*
# 
# ==================================================================
# Additions to docker image: 2019-Oct-10
# Latex, seaborn, pandas-profiling
# ==================================================================
# 
# ==================================================================
# LaTeX
# ------------------------------------------------------------------
# 	
    Run apt install texlive-base -y --no-install-recommends
# 	
# 
