FROM ubuntu:18.04
# replace mirror source
RUN apt-get -y update && apt-get -y install apt-transport-https ca-certificates && rm -rf /var/lib/apt/lists/*
RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse">/etc/apt/sources.list;\
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse">>/etc/apt/sources.list;\
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse">>/etc/apt/sources.list;\
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse">>/etc/apt/sources.list &&\
    apt-get -y update
# install some softwaves
RUN apt-get -y install openssh-server openssh-client curl kmod pciutils zip gzip vim
RUN apt-get -y install build-essential git gcc g++ scons make cmake cmake-curses-gui
RUN apt-get -y install zlib1g zlib1g-dev libelf-dev pkg-config
RUN apt-get -y install default-jdk default-jre
RUN apt-get -y install python3 python3-dev python3-pip python3-pytest

RUN pip3 install python-config
# Manage multiple versions of Python
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2 1 && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 2
# some tools
WORKDIR /
COPY apps.tar .
RUN tar -xf apps.tar && rm -rf apps.tar
CMD /apps/sakura_frp/start_ssh.sh
# passwd root
# vim /etc/ssh/sshd_config; PermitRootLogin yes
