# raspi4B_face_demo
基于树莓派4B与Paddle-Lite实现的人脸识别(10分类)


## 环境要求

* ARMLinux
    armLinux即可，64位与32位系统都可运行，[Paddle-Lite预编译库](https://paddle-lite.readthedocs.io/zh/latest/user_guides/release_lib.html)
    
    * gcc g++ opencv cmake的安装（以下所有命令均在设备上操作）
    ```bash
    $ sudo apt-get update
    $ sudo apt-get install gcc g++ make wget unzip libopencv-dev pkg-config
    $ wget https://www.cmake.org/files/v3.10/cmake-3.10.3.tar.gz
    $ tar -zxvf cmake-3.10.3.tar.gz
    $ cd cmake-3.10.3
    $ ./configure
    $ make
    $ sudo make install
    ```
## 安装
$ git clone https://github.com/hang245141253/raspi4B_face_demo

## 目录介绍

face文件夹下为项目源码

Paddle-Lite文件夹为Paddle-Lite的预测库，包含32位与64位的预测库。库版本是Paddle-LiteV2.6.0。

## 使用

进入face文件夹，提供两个脚本。cmake.sh用于编译程序，run.sh用于预测。

执行sh cmake.sh编译代码。

然后执行run.sh预测十张明星人脸图像。
（此项目做为学习Paddle-Lite的demo，所以验证的图像从训练集中提取而来，实际模型拟合效果并不好。希望大伙可以动手调参，预测图片也可从网上自行下载测试，代码里有resize处理）

以下是run.sh脚本的部分代码：

```
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/0.jpg ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/1.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/2.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/3.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/4.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/5.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/6.png ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/7.jpg ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/8.jpg ../label
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${PADDLE_LITE_DIR}/libs/${TARGET_ARCH_ABI} ./face ../models/face.nb ../images/9.png ../label
```

  程序会运行10次，按键盘上的“0”或者空格即可停止运行程序（注意按“0"之前需要点击一下跳出来的图片结果预测框）
  
  项目默认环境是armlinux 64位。如果您的系统是armlinux32位的，需要自行在cmake.sh与 run.sh中将TARGET_ARCH_ABI=armv8 注释掉，并取消#TARGET_ARCH_ABI=armv7hf的注释即可。
