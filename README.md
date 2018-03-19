# How to upgrade to tensorflow1.6 on Ubuntu 16.04
### (with cuda9.1, cudnn7.0.5 and NVIDIA driver 390.30)
## Install cuda

   Follow the [link](https://developer.nvidia.com/cuda-downloads)
    
## Install cudnn
1. Register NVIDIA [account](https://developer.nvidia.com/rdp/cudnn-download)
2. Log in and download cudnn package 
   1. **cuDNN v7.0.5 Library for Linux**
   2. **cuDNN v7.0.5 Runtime Library for Ubuntu16.04 (Deb)**
   2. **cuDNN v7.0.5 Developer Library for Ubuntu16.04 (Deb)**
   2. **cuDNN v7.0.5 Code Samples and User Guide for Ubuntu16.04 (Deb)**
3. Install
```
    sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
    sudo dpkg -i libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
    sudo dpkg -i libcudnn7-doc_7.0.5.15-1+cuda9.0_amd64.deb

    tar -xzvf cudnn-9.1-linux-x64-v7.tgz
    sudo cp cuda/include/*.h /usr/local/cuda/include
    sudo cp cuda/lib64/*.so* /usr/local/cuda/lib64
    sudo ldconfig /usr/local/cuda/lib64/
```

## Upgrade tensorflow
```
   sudo pip3 install tensorflow-gpu --upgrade
```

## Problems encountered and solution
1. >Error: CUDNN_STATUS_INTERNAL_ERROR
```
   sudo rm -rf ~/.nv
```
2. >Loaded runtime CuDNN library: 7101 (compatibility version 7100) but source was compiled with 7004 (compatibility version 7000).

      Don't use cuDNN v7.1, install cuDNN v7.0, remove ```usr/local/cuda/lib64/libcudnn.so.7.1.1``` if necessary

3. >libcudnn.so.7 is not a symbolic link

```   
    sudo ldconfig /usr/local/cuda/lib64/
```

## Useful setting
1. NVIDIA Fan setting
```
    sudo nvidia-xconfig --enable-all-gpus
    sudo nvidia-xconfig --cool-bits=4
    sudo reboot
```
2. NVIDIA graphic card status
```
    nvidia-smi
```
3. check Cuda version
```
    nvcc  --version
```
4. check Cudnn version
```
    cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```
5. make python3 as default
   1. ```vim ~/.bashrc```
   2. add this in the file: ```alias python=python3``` 
   3. ```source ~/.bashrc```
