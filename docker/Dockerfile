# ref https://github.com/tebeka/pythonwise/blob/master/docker-miniconda/Dockerfile
FROM py_base_on_ubu18:3.8.3

ENV PYTHON_VERSION 3.8.3
ENV DEBIAN_FRONTEND=noninteractive
ENV HOME /root
ENV PYTHON_ROOT $HOME/local/python-$PYTHON_VERSION
ENV PATH $PYTHON_ROOT/bin:$PATH
ENV PYENV_ROOT $HOME/.pyenv

# install packages in requirements.txt
ADD requirements.txt ./
RUN pip install -r requirements.txt    # requirements.txtからパッケージのインストール

# nodejsの導入
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - \
    && sudo apt-get install -y nodejs

## JupyterLabの拡張機能
RUN jupyter labextension install @lckr/jupyterlab_variableinspector \
    && jupyter labextension install @jupyterlab/toc

# 自動整形
RUN pip install autopep8 \
    && pip install jupyterlab_code_formatter \
    && jupyter labextension install @ryantam626/jupyterlab_code_formatter \
    && jupyter serverextension enable --py jupyterlab_code_formatter

