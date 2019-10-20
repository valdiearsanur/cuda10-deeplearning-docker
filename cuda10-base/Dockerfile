# MAINTAINER valdiearsanur <valdiearsanur@yahoo.fr>
FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04
ENV LANG C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \
    touch /root/.bash_profile && \
    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get update

# ==================================================================
# tools
# ------------------------------------------------------------------

RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        build-essential \
        screen \
        apt-utils \
        libsqlite3-dev \
        ca-certificates \
        wget \
        git \
        vim \
        libssl-dev \
        curl \
        unzip \
        unrar \
        python-pydot \
        python-pydot-ng \
        graphviz \
        && \
    $GIT_CLONE https://github.com/Kitware/CMake ~/cmake && \
        cd ~/cmake && \
        ./bootstrap && \
        make -j"$(nproc)" install && \
    $GIT_CLONE https://github.com/Bash-it/bash-it.git ~/.bash_it && \
        ~/.bash_it/install.sh --silent && \
        echo "if [ -f /root/.bashrc ]; then\n  . /root/.bashrc\nfi" >> /root/.bash_profile
        # source /root/.bash_profile

# ==================================================================
# python
# ------------------------------------------------------------------

RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \
    $APT_INSTALL \
        software-properties-common \
        && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        python3.6 \
        python3.6-dev \
        python3-distutils-extra \
        && \
    wget -O ~/get-pip.py \
        https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ~/get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    $PIP_INSTALL \
        setuptools

# ==================================================================
# miniconda
# ------------------------------------------------------------------

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda2-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc


#RUN curl -LO http://repo.continuum.io/miniconda/Miniconda-latest-Linux-x86_64.sh && \
#        bash Miniconda-latest-Linux-x86_64.sh -b -p ~/miniconda && \
#        rm Miniconda-latest-Linux-x86_64.sh && \
#        ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
#        echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
#        echo "conda activate base" >> ~/.bashrc
#        echo "PATH=\$PATH:\$HOME/miniconda/bin" >> /root/.bash_profile && \
        # source /root/.bash_profile && \
        # conda update -y conda

# ==================================================================
# config & cleanup
# ------------------------------------------------------------------

RUN ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*
