# srpip

#记录srpip开始以来遇到的坑与操作
硬件： 树莓派4B 4GB、树莓派摄像头V2
系统：raspbain  buster系统

配置换源（最重要，不然更新一下等千年）：
打开终端：sudo nano etc/apt/sources.list 
将里面的内容注释掉后 
更换源为：deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
#deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi（这里使用中科大源、也可以使用清华、阿里等源）
ctrl+o 保存  enter 确认文件名  ctrl + x退出

sudo nano /etc/apt/sources.list.d/raspi.list
注释后
更换源为
deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/ buster main ui（依旧以中科大源为例）

sudo apt-get update&&sudo apt-get upgrade更新一下
！！ 每次安装依赖或是开机之后最好都sudo apt-get update&&sudo apt-get upgrade更新一下，会少很多诡异的问题

安装dlib
各种依赖和需求：
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
会有点时间，完全配置成国内的镜像源就会快很多很多很多很多

安装具有阵列支持的picamera python库：

sudo apt-get install python3-picamera
sudo pip3 install --upgrade picamera[array]

临时启用的交换空间（内存不够用的时候用，但4b 4gb版本没有这个问题）：

sudo nano /etc/dphys-swapfile

< change CONF_SWAPSIZE=100 to CONF_SWAPSIZE=1024 and save / exit nano >

sudo /etc/init.d/dphys-swapfile restart

下载dlib v19.7

mkdir -p dlib
git clone -b 'v19.7' --single-branch https://github.com/davisking/dlib.git dlib/
cd ./dlib
sudo python3 setup.py install --compiler-flags "-mfpu=neon"

会要很久，慢慢等，face_recognition官方说的19.6版本和buster不匹配，要用19.7

安装face_recognition：
sudo pip3 install face_recognition
好像没什么用，经常超时，建议去wheel官网下载whl本地安装


