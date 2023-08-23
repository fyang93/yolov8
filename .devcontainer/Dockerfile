FROM ultralytics/ultralytics:latest

ARG USERNAME
ARG USER_UID
ARG USER_GID=$USER_UID

ENV HOME /home/$USERNAME
ENV SHELL /bin/bash

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt update \
    && apt upgrade --no-install-recommends -y \
    && apt install --no-install-recommends -y sudo wget tmux \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && apt autoremove -y \
    && apt clean -y \
    && rm -rf /var/lib/apt/lists/*

USER $USERNAME
# WORKDIR $HOME

# COPY ./requirements.txt /tmp/
# RUN pip install --upgrade pip \
#     && pip install --user --no-cache-dir -r /tmp/requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple