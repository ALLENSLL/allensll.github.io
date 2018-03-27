---
layout: post
title: A note about installing tensorflow
---

Recently, I want to use a pre-trained faster-rcnn to finish a persion dection task. As a beginner of Deep learning, I need to install Tensorflow in my computer, and it took me two days, so I decid to record the installation steps.

[Tensorflow's Official Guide](https://www.tensorflow.org/install/) is the first and the most important doc you should read.

### My device and version
* Ubuntu 16.04
* GeForce GT 710
* CUDA Toolkit 9.0
* cuDNN v7.0.5
* Python 3.6
* Tensorflow 1.6

### Step 1 installing OS

Tensorflow certainlly supports all commmon OS, and I choice Ubuntu 16.04 whitch same as official guide. There are two things need to be concerned

* If you use a WiFi adapter to connect network, you should plug adapter into computer before run the installer, and then installer will automatically install and load suitable kernel modules.

* CUDA Toolkit 9.0 request at least Kernel 4.4 for Ubuntu 16.04, so I should update Kernel after install Ubuntu. All mainline kernel build can be downloaded [here](http://kernel.ubuntu.com/~kernel-ppa/mainline/) you can use wget command to download kernel.
```Shell
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.4.124/ \
linux-headers-4.4.124-0404124_4.4.124-0404124.201803250430_all.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.4.124/ \
linux-headers-4.4.124-0404124-generic_4.4.124-0404124.201803250430_amd64.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.4.124/ \
linux-image-4.4.124-0404124-generic_4.4.124-0404124.201803250430_amd64.deb
```
install the packages.
```Shell
dpkg -i *.deb
```
update grub and reboot the system.
```Shell
sudo update-grub
sudo reboot
```
check the kernel version.
```Shell
uname -r
```

### Step 2 installing NVIDIA software

In this step, two software, [CUDA Toolkit](http://docs.nvidia.com/cuda/) and [cuDNN](https://developer.nvidia.com/cudnn) will be installed, but first verify you have a CUDA-Capable GPU and Tensorflow only support whitch **compute capability >= 3.0**. See [here](https://developer.nvidia.com/cuda-gpus) for a list of supported GPU cards. I don't find GT 710 in that list, so just google GT 710 to find the answer.

* **installing CUDA Tookit 9.0**. The NVIDIA drivers associated with CUDA Toolkit, so don't need to install it alone. It is easy to encounter problems at this step.
    1. Check prerequisite before install.
    1. Download the [NVIDIA CUDA Toolkit](http://developer.nvidia.com/cuda-downloads)
    1. Disable Noveau drivers.<br>
    pushing `Ctrl`+`Alt`+`F1` and login,<br>
    type `sudo service lightdm stop`,<br>
    create a file: `/etc/modprobe.d/blacklist-nouveau.conf` and type follow:
    ```Shell
    blacklist nouveau
    options nouveau modeset=0
    ```
    reboot and verify Noveau not loaded.
    ```Shell
    lsmod | grep nouveau
    ```
    1. install cuda.
    ```Shell
    sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
    sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub
    sudo apt-get update
    sudo apt-get install cuda
    ```
    1. reboot and check install
    ```Shell
    nvidia-smi
    nvcc --version
    ```

* **installing cuDNN v7.0.5**. Read [cuDNN Installation Guide](http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html) to learn more detials.
    1. Check prerequisite before install.
    1. download [cuDNN](https://developer.nvidia.com/cudnn).
    1. install cuDNN.
    ```Shell
    sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
    ```
    1. set path variables. Add these lines to end of `/etc/profile` and reboot
    ```Shell
    export PATH=/usr/local/cuda/bin${PATH:+:PATH}
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64
    export CUDA_HOME=/usr/local/cuda
    ```

### Step 3 installing Tensorflow

I use Anaconda environment to use Tensorflow, type the following instructions.
```Shell
conda create -n tensorflow pip python=3.6
source activate tensorflow
pip install tensorflow-gpu -i https://pypi.tuna.tsinghua.edu.cn/simple
```

### Step 4 test Tensorflow

type the following python code to test Tensorflow.
```Python
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print sess.run(hello)
# Hello, TensorFlow!
```

#### *External links*
* [https://blog.csdn.net/zhaoyu106/article/details/52793183](https://blog.csdn.net/zhaoyu106/article/details/52793183)
* [https://github.com/williamFalcon/tensorflow-gpu-install-ubuntu-16.04](https://github.com/williamFalcon/tensorflow-gpu-install-ubuntu-16.04)

<br>