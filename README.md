# Install-DeepLearning-GPU-R

This tutorial to get tensorflow-gpu working in R was realized in Ubuntu 18.04 LTS

### 1st step: Check NVIDIA driver version

Check if your graphic card is Cuda-GPU enabled: https://developer.nvidia.com/cuda-gpus

Check your graphic card and the nvidia driver version installed in your computer

_$ nvidia-smi_

If you don't have the nvidia driver, you can download the required driver for your graphic card from here: https://www.nvidia.com/Download/index.aspx?lang=en-us

### 2nd step: Install the CUDA Toolkit

You can download the Cuda Toolkit from:

https://developer.nvidia.com/cuda-90-download-archive? (Cuda 9 recommended) <br>
https://developer.nvidia.com/cuda-downloads (Cuda 10) <br>

I recommended Cuda 9 because TensorFlow don't support 10 version: https://www.tensorflow.org/install/source#tested_build_configurations <br>

Once you download it, it is important to follow the installation instructions provided in the web (to install also the keys)

_$ sudo dpkg -i cuda-repo-ubuntu1704-9-0-local_9.0.176-1_amd64.deb_
_$ sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub_
_$ sudo apt-get update_
_$ sudo apt-get install cuda_  

### 3rd step

### References
