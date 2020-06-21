---
title: "GTX1050ti tensorflow-gpu==1.14"
date: 2020-06-21 20:04:10 -0400
categories: tensorflow
---
```
conda install -y python==3.6.9
tensorflow-gpu==1.14
keras==2.3.0
CUDA=10.0
```
[기본가이드](https://medium.com/@redowan/no-bullshit-guide-on-installing-tensorflow-gpu-ubuntu-18-04-18-10-238924cc4a6a)

[텐서플로우 홈페이지 gpu 설치](https://www.tensorflow.org/install/gpu?hl=ko)

[CUDA downgrade](https://teddylee777.github.io/linux/CUDA-%EC%9D%B4%EC%A0%84%EB%B2%84%EC%A0%84-%EC%82%AD%EC%A0%9C%ED%9B%84-%EC%9E%AC%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)

[텐서플로우 gpu 사용 여부 확인](https://teddylee777.github.io/tensorflow/%EB%94%A5%EB%9F%AC%EB%8B%9D-framework-GPU%EC%82%AC%EC%9A%A9%EC%B2%B4%ED%81%AC-API)

[conda PermissionError 13](https://stackoverflow.com/questions/49092807/when-conda-install-django-permissionerror13-permission-denied)







#### Blacklist the driver
```
sudo bash -c "echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
sudo bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
```
#### Confirm the content of the new modprobe config file
```
cat /etc/modprobe.d/blacklist-nvidia-nouveau.conf

blacklist nouveau
options nouveau modeset=0
```
#### Update kernel initramfs
```
sudo update-initramfs -u
```
#### Reboot
```
sudo reboot
```
#### Remove Any Other NVIDIA Driver
##### Add the graphics driver PPA
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
#### Purge the driver
```
sudo apt-get purge nvidia* && sudo apt-get autoremove && sudo apt-get autoclean && sudo rm -rf /usr/local/cuda*
```
#### Reboot
```
sudo reboot
```
#### Add Nvidia package repositories
```
# Add NVIDIA package repositories
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo apt-get update
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt-get update
```
#### Install Nvidia driver
```
sudo apt-get install --no-install-recommends nvidia-driver-418
```
#### Reboot
```
sudo reboot
```
#### Install Runtime & Development Libraries (cuDNN)
```
sudo apt-get install --no-install-recommends cuda-10-0 libcudnn7=7.6.2.24-1+cuda10.0 libcudnn7-dev=7.6.2.24-1+cuda10.0
```
#### Install TensorRT
```
sudo apt-get install -y --no-install-recommends libnvinfer5=5.1.5-1+cuda10.0 libnvinfer-dev=5.1.5-1+cuda10.0
```
#### check nvidia
```
# 설치된 nvidia-smi
nvidia-smi
# nvcc로 cuda의 버전체크
nvcc --version
```

#### Install Anaconda package
[click here](https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh)
#### If conda has permission error 13
```
sudo chown -R user anaconda3
```
#### conda python3
```
conda install -y python==3.6.9
```
#### vertural env
```
conda create -n tf-gpu3.6.9 python=3.6.9
source activate  tf-gpu3.6.9
```
#### tensorflow & keras install
```
conda install tensorflow-gpu==1.14
conda install keras==2.3

# 아래 세개는 자동 설치 되더라.
conda install cudatoolkit==9.0
conda install cudatoolkit==7.1.2
conda install h5py
```









Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
