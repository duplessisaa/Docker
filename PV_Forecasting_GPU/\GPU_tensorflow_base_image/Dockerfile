#
# Source: Leanne Nortje, 2019
# Edited: Armand du Plessis
# Read: https://hub.docker.com/r/tensorflow/tensorflow/
#_____________________________________________________________________________________________________________________________________

# Parent image is docker image for TensorFlow 
FROM tensorflow/tensorflow:1.13.1-gpu-py3-jupyter

# Standard tools (Python 3.6)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        less \
        nano \
        git \
        && \
    python -m pip --no-cache-dir install --upgrade \
        setuptools==40.8.0 \
        pip==19.1.1 \
        && \
    python -m pip --no-cache-dir install --upgrade \
        numpy \
        scipy \
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
        Cython==0.29.4\
		tables==3.4.4 \

# LaTeX config
RUN tlmgr install collection-fontsrecommended

# Working directory
WORKDIR /home

CMD ["bash"]
