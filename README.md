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

I recommended Cuda 9 because TensorFlow don't support 10 version: https://www.tensorflow.org/install/source#tested_build_configurations

### 3rd step

### References
