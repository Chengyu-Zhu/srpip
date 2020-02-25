# srpip

Srpip 

硬件：树莓派4B 4GB、树莓派摄像头v2、sense HAT
系统：raspbain buster（debian 10）

安装face_recognition 库
换源：（中科大的会快些）
# 编辑 `/etc/apt/sources.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main non-free contrib

# 编辑 `/etc/apt/sources.list.d/raspi.list` 文件，删除原文件所有内容，用以下内容取代：
deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui


所需前提库的安装：
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential \
    cmake \
    gfortran \
    git \
    wget \
    curl \
    graphicsmagick \
    libgraphicsmagick1-dev \
    libatlas-dev \
    libavcodec-dev \
    libavformat-dev \
    libboost-all-dev \
    libgtk2.0-dev \
    libjpeg-dev \
    liblapack-dev \
    libswscale-dev \
    pkg-config \
    python3-dev \
    python3-numpy \
    python3-pip \
    zip
sudo apt-get clean

picamera的更新：

sudo apt-get install python3-picamera
sudo pip3 install --upgrade picamera[array]

下载安装dlib的‘19.7.0’版本适用于python3.7：

mkdir -p dlib
git clone -b 'v19.7' --single-branch https://github.com/davisking/dlib.git dlib/
cd ./dlib
sudo python3 setup.py install --compiler-flags "-mfpu=neon"
会很慢要等一会

安装face_recognition：

sudo pip3 install face_recognition

pip下载太慢的时候，直接去镜像网站下tar.gz 压缩包或者whl文件安装：

pip3 setup.py install(tar.gz解压后在文档目录下)

pip3 install xxxxxx.whl (给whl用，也要在文档目录下)

Opencv的安装  ：

各种相关的依赖包：

升级更新软件包：
sudo apt-get update 
sudo apt-get upgrade

安装图像I/O包：
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng-dev

安装视频I/O包，方便获取 视频流：
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev

为编译 highgui模块，我们需要安装GTK开发库：

sudo apt-get install libfontconfig1-dev libcairo2-dev
sudo apt-get install libgdk-pixbuf2.0-dev libpango1.0-dev
sudo apt-get install libgtk2.0-dev libgtk-3-dev


安装一些额外项来优化opencv许多内部操作（如矩阵操作）：
sudo apt-get install libatlas-base-dev gfortran


安装适用于HDF5数据集和Qt GUI：
sudo apt-get install libhdf5-dev libhdf5-serial-dev libhdf5-103
sudo apt-get install libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5

安装opencv：

pip3 install opencv-contrib-python
还是建议直接去镜像网站找到合适的安装包（树莓派4版本为 armhf或者 armv7）

安装虚拟空间的包（类似于anaconda）：

sudo pip3 install virtualenv virtualenvwrapper

打开 ~/.bashrc 文件：
sudo nano ~/.bashrc

添加：
#virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
保存退出

重新加载source一下bashrc：
source ~/.bashrc

Python 3 创建一个名为py3（可自己随便起）的Python虚拟环境：
mkvirtualenv py3 -p python3

激活py3环境：
workon py3
