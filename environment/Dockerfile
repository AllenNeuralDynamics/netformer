# hash:sha256:b8ee6b1fbb726112ca5d9d4b38e7c30d248a58d0bbb2ded14c6df82ff139c92b
ARG REGISTRY_HOST
#FROM $REGISTRY_HOST/codeocean/jupyterlab:3.0.9-miniconda4.9.2-python3.8-ubuntu20.04
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

# fonts for gifs
RUN apt-get update -y
RUN apt install fonts-lato fonts-open-sans fonts-roboto fonts-mononoki -y

# for pyqt5 in ubuntu22.04 (to run suite2p GUI)
# RUN apt-get update && apt-get install -y build-essential git cmake && rm -rf /var/lib/apt/lists/*
# RUN apt-get update && apt-get install -y libsndfile1-dev libjack-jackd2-dev libfftw3-dev && rm -rf /var/lib/apt/lists/*
# RUN apt-get update && apt-get install -y emacs libudev-dev && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y qtbase5-dev qt5-qmake qttools5-dev qttools5-dev-tools && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y qtwebengine5-dev libqt5svg5-dev libqt5websockets5-dev && rm -rf /var/lib/apt/lists/*

#RUN apt install build-essential git cmake libsndfile1-dev libjack-jackd2-dev libfftw3-dev emacs libudev-dev
#RUN apt install qtbase5-dev qt5-qmake qttools5-dev qttools5-dev-tools qtwebengine5-dev libqt5svg5-dev libqt5websockets5-dev

RUN pip install -U --no-cache-dir \
    matplotlib \
    numpy \    
    scipy \
    pandas \
    aind-codeocean-utils \
    aind-data-access-api \
    aind-ophys-utils \
    ipykernel \
    scikit-learn \
    aind_session

RUN cd / \
    && git clone https://github.com/AllenNeuralDynamics/aind-codeocean-api \
    && cd aind-codeocean-api \
    && pip install -e .

RUN cd / \
    && git clone https://github.com/AllenNeuralDynamics/aind-ophys-data-access \
    && cd aind-ophys-data-access \
    && pip install -e .

RUN cd / \
    && git clone https://github.com/AllenNeuralDynamics/comb \
    && cd comb \
    && pip install -e .

RUN cd / \
    && git clone https://github.com/AllenNeuralDynamics/lamf-analysis \
    && cd lamf-analysis \
    && pip install -e .

RUN cd / \
    && git clone https://github.com/NeuroAIHub/NetFormer.git \
    && cd NetFormer \
    && pip install -e .


COPY postInstall /
RUN /postInstall
