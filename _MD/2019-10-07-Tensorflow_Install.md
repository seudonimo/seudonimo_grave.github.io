---
layout: pos"
title: "Tensorflow 설치법""
author: "seudonimo"
tag: [tensorflow]
---

# Tensorflow-GPU on Ubuntu 18.04

매번 설치할 때마다 버전이 조금씩 바뀌고 엇갈리다보니 몇일 씩 소비하는거 같다. 특히나 NVIDIA(GPU Driver + CUDA + CUDNN)설치 때, 많은 가이드 문서들이 재부팅을 해서 lightdm와 nouveau를 끄고 설치를 해야 하는 등 복잡하지만 이 방법은 복잡하지 않고 apt로 간단하게 설치 할 수 있어서 별도로 기록 해두고 싶었다.

<https://hiseon.me/data-analytics/tensorflow/tensorflow-install/>

대략적인 설치 순서는 아래와 같다.

##### 설치 순서

1. Check GPU Specification
2. Install GPU Driver
3. Install CUDA, CuDNN
4. Install Tensorflow-GPU
5. Check Code



### Check GPU Specification

먼저 설치하려는 컴터에 장착된 NVIDIA GPU의 사양을 알아본다. "***ubuntu-drivers devices***"로 확인하니, 내 컴터에 설치된 GPU는 GTX 1070이며, 추천하는 driver는 "***nvidia-driver-430***"이라고 한다.

```bash
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:03.1/0000:09:00.0 ==
modalias : pci:v000010DEd00001B81sv000010DEsd00001B81bc03sc00i00
vendor   : NVIDIA Corporation
model    : GP104 [GeForce GTX 1070]
driver   : nvidia-driver-430 - distro non-free recommended
driver   : nvidia-driver-410 - third-party free
driver   : nvidia-driver-390 - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```



### Install GPU Driver

##### repository를 추가

```bash
$ release="ubuntu"$(lsb_release -sr | sed -e "s/\.//g")
$ echo $release

$ sudo apt install sudo gnupg
$ sudo apt-key adv --fetch-keys "http://developer.download.nvidia.com/compute/cuda/repos/"$release"/x86_64/7fa2af80.pub"
$ sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/'$release'/x86_64 /" > /etc/apt/sources.list.d/nvidia-cuda.list'
$ sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/'$release'/x86_64 /" > /etc/apt/sources.list.d/nvidia-machine-learning.list'
$ sudo apt update
```



##### 해당 드라이버가 설치 가능한지 확인 & 설치

추천 받은 버전(내 경우엔 430)의 드라이버가 설치 가능한 버전인지 확인하고 설치한다. 그리고 driver가 등록되도록 reboot 한다.

```bash
$ sudo apt-cache search nvidia | grep nvidia-driver-430
nvidia-driver-418 - Transitional package for nvidia-driver-430
nvidia-driver-430 - NVIDIA driver metapackage
$ sudo apt-get install nvidia-driver-430
....
$ sudo reboot
```



##### 설치 확인

nvidia GPU 드라이버가 정상적으로 설치되었다면 아래와 같이 driver version, cuda version이 확인 될 것이다. 

```bash
$ nvidia-smi
Tue Oct  1 21:24:38 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 430.26                 Driver Version: 430.26                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1070    Off  | 00000000:09:00.0  On |                  N/A |
|  0%   38C    P8     7W / 195W |    143MiB /  8116MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1231      G   /usr/lib/xorg/Xorg                            57MiB |
|    0      1276      G   /usr/bin/gnome-shell                          83MiB |
+-----------------------------------------------------------------------------+ 
```



### Install CUDA, CuDNN

CUDA 설치 전에,  GPU에서 설치 가능한 [CUDA 버전을 확인](https://developer.nvidia.com/cuda-gpus) 한다. 이 문서에선 CUDA 10을 설치한다. 위 챕터에서 이미 repository를 추가했으므로 바로 설치한다,

```bash
$ sudo apt-get install cuda-10-0
$ sudo apt-get install libcudnn7-dev
```



##### 설치확인

설치된 CUDA, CuDNN의 버전을 확인한다.

```bash
$ cat /usr/local/cuda/version.txt
CUDA Version 10.0.130

$ cat /usr/include/cudnn.h | grep -E "CUDNN_MAJOR|CUDNN_MINOR|CUDNN_PATCHLEVEL"
#define CUDNN_MAJOR 7
#define CUDNN_MINOR 6
#define CUDNN_PATCHLEVEL 4
#define CUDNN_VERSION (CUDNN_MAJOR * 1000 + CUDNN_MINOR * 100 + CUDNN_PATCHLEVEL)

```



### Install Tensorflow-GPU

마지막이다.

```bash
$ sudo pip install tensorflow-gpu
```



##### 설치확인

정상적으로 설치가 되었다면 

```bash
$ python -c 'import tensorflow as tf; print(tf.__version__)'
...
1.14.0
$
```

