# AAMLP
AAMLP ... Approaching (Almost) Any Machine Learning Probrem  

[This book](https://www.amazon.com/Approaching-Almost-Machine-Learning-Problem-ebook/dp/B089P13QHT) is published by [ABHISHEK THAKUR](https://www.kaggle.com/abhishek) - one and only guy who has Quadruple Grand Master on Kaggle.  

- His [Article at Linkedin - Approaching (Almost) Any Machine Learning Problem](https://www.linkedin.com/pulse/approaching-almost-any-machine-learning-problem-abhishek-thakur/)
- His [Presentation documents at KaggleDays19 at slideshare - Approaching (almost) Any Machine Learning Problem (kaggledays dubai)](https://www.slideshare.net/abhishekkrthakur/approaching-almost-any-machine-learning-problem-kaggledays-dubai)

# requirements.txt
ALL I NEED is this book and the list of `requirements.txt` file for python/docker. I checked the libraries required in all code in this book, and listed them. Please use this `requirements.txt` file for your training.  

# docker
I used docker for build the coding environment, and put the files in this repository, too. In `Dockerfile`, I use the image file named `py_base_on_ubu18:3.8.3` - it's just image file included Ubuntu18.04+Python3.8.3 with no additional libraries. If you need it, use code below:  

`docker build ./ -t py_base_on_ubu18:3.8.3`

```
# Dockerfile for make py_base_on_ubu18:3.8.3

FROM ubuntu:18.04

ENV PYTHON_VERSION 3.8.3
ENV DEBIAN_FRONTEND=noninteractive
ENV HOME /root
ENV PYTHON_ROOT $HOME/local/python-$PYTHON_VERSION
ENV PATH $PYTHON_ROOT/bin:$PATH
ENV PYENV_ROOT $HOME/.pyenv

# install pyenv for allowing to install any python
RUN apt-get update && apt-get upgrade -y \
 && apt-get install -y \
    git \
    make \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    wget \
    curl \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libffi-dev \
    liblzma-dev \
 && git clone https://github.com/pyenv/pyenv.git $PYENV_ROOT \
 && $PYENV_ROOT/plugins/python-build/install.sh \
 && /usr/local/bin/python-build -v $PYTHON_VERSION $PYTHON_ROOT \
 && rm -rf $PYENV_ROOT

# install pip and locales
RUN apt-get -y update \
    && apt-get -y upgrade \
    && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
    && python get-pip.py \
    && pip install -U pip \
    && apt-get install -y sudo curl wget locales \
    && rm -rf /var/lib/apt/lists/* \
    && echo "ja_JP UTF-8" > /etc/locale.gen \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
```

If you need `Dockerfile` and `docker-compose.yml`, then use it after move `requirements.txt` into `./docker/` . I build the container utilizing VSCode, so usually I use `.devcontainer`
