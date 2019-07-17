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

_$ sudo dpkg -i cuda-repo-ubuntu1704-9-0-local_9.0.176-1_amd64.deb_ <br>
_$ sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub_ <br>
_$ sudo apt-get update_ <br>
_$ sudo apt-get install cuda_ <br>  

Now, you can check the Cuda version (normally in /usr/local/cuda):

_$ cat /usr/local/cuda/version.txt_

Check the nvcc compiler:

_$ nvcc --version_

And the cuda installation:

_$ cd /usr/local/cuda-9.0/samples/1_Utilities/deviceQuery_ <br>
_$ sudo make_ <br>
_$ ./deviceQuery_ <br>


### 3rd step: Install CUDNN

You can download the cuda deep neural network library from here (nvidia login requested): https://developer.nvidia.com/cudnn

You should select the download for the previous installed cuda version and download:

cuDNN v7.x.x Library for Linux <br>
cuDNN v7.x.x Runtime Library for Ubuntuxx.xx (Deb) <br>
cuDNN v7.x.x Developer Library for Ubuntuxx.xx (Deb) <br>
cuDNN v7.x.x Code Samples and User Guide for Ubuntuxx.xx (Deb) <br>

Once downloaded, unpack the first archive and copy the following files to local cuda distribution:

_$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include_ <br>
_$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64_ <br>

Give read access to all users:

_$ sudo chmod a+r /usr/local/cuda-9.0/include/cudnn.h /usr/local/cuda/lib64/libcudnn*_ <br>
_$ sudo chmod a+r /usr/local/cuda/include/cudnn.h_ <br>

Next, install in this order:

_$ sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb_ <br>
_$ sudo dpkg -i libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb_ <br>
_$ sudo dpkg -i libcudnn7-doc_7.0.5.15-1+cuda9.0_amd64.deb_ <br>

And finally, install the nvidia cuda Profile Tools:

_$ sudo apt-get install libcupti-dev_

Check the cudnn installation:

_$ cd /usr/src/cudnn_samples_v7/_ <br>
_$ cd cudnn_samples_v7/mnistCUDNN_ <br>
_$ make clean && make_ <br>
_$ sudo ./mnistCUDNN_ <br> 



### 4th step: Cuda path

To ensure that Tensorflow can find your CUDA installation and use it properly, you need to add the path to the CUDA binaries to your PATH and LD_LIBRARY_PATH _(for more information see the references)_.

It's important to modify the .profile if you will use RStudio, otherwise the .bashrc file.

Example; In .profile or in .bashrc add:
  export CUDA_HOME=/usr/local/cuda/
  export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:${CUDA_HOME}/lib64 
  PATH=${CUDA_HOME}/bin:${PATH} 
  export PATH



### 5th step: Install Keras and TensorFlow in R

Install keras from github repository (in R console):

_devtools::install_github("rstudio/keras")_

Install tensorflow in gpu (in R console):

_keras::install_keras(tensorflow = "gpu")_

Example for verifying correct operation:

_library(keras)_ <br>
_library(tensorflow)_ <br>

_sess = tf$Session()_ <br>
_hello <- tf$constant('Hello, TensorFlow!')_ <br>
_sess$run(hello)_ <br>




### Extra: Select GPU in R

By default, R selects GPU0 to compute and allocates the memory in all GPUs availables (GPU0, GPU1, ...). For use only one specific GPU and not the others, we have to change the devices visibles in cuda: 

_Sys.setenv(CUDA_VISIBLE_DEVICES = "0")_ <br>

In this way, the others GPU devices will be availables for new executions at the same time. De otra manera, si quieres calcular usando todas las GPUs, también es posible:

https://keras.rstudio.com/articles/faq.html#how-can-i-run-a-keras-model-on-multiple-gpus <br>
https://keras.rstudio.com/reference/multi_gpu_model.html <br>



### References

https://tensorflow.rstudio.com/tools/local_gpu.html <br>
https://medium.com/@taylordenouden/installing-tensorflow-gpu-on-ubuntu-18-04-89a142325138 <br>
https://medium.com/codezillas/step-by-step-guide-to-install-tensorflow-gpu-on-ubuntu-18-04-lts-6feceb0df5c0 <br>
https://sndean.github.io/blog/2018/03/10/setting-up-keras-for-r-configured-to-run-on-gpus/ <br>
https://medium.com/intro-to-artificial-intelligence/install-tensorflow-gpu-on-ubuntu18-04-ff311a8bd4d6 <br>
