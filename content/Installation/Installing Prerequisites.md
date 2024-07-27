---
tags:
  - installation
  - getting-started
  - tutorials
custom-width: .nan
---
# Prerequisites
# Prerequisites
> [!CAUTION]
> For Windows users, WSL2 is needed to run LEIP SDK. We currently do not support native Windows.

As a general supportability statement, any OS that has Docker installed with access to a CUDA-enabled GPU can utilize LEIP SDK.

For our testing, we have used:
* Linux-based system (Ubuntu 20.04 or 22.04)  
* NVIDIA GPU (from CUDA 10 to CUDA 12).  
* Docker 1.19 or greater

## Useful Prerequisite Links
### Ubuntu
* [Create an Ubuntu Installation USB & Install Ubuntu](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows/#1-overview)
	* Note: [[#Step 1 Installing NVIDIA Drivers]] can be achieved by simply enabling the installation of third-party drivers, as this will automatically install NVIDIA drivers. [[ubuntu-install-third-party.png|Click here]] to view where this can be checked off.
### Windows


# Step 1: Installing NVIDIA Drivers

## Ubuntu
1. Once you have booted into the OS, open a terminal to update packages.
	```
	sudo apt update
	sudo apt -y upgrade
	sudo apt -y autoremove
	```

2. Check to see if you have your NVIDIA driver installed. A printout similar to the snippet below will signify a successful detection of your GPU.  
	1. If you are not able to see this, refer to [this link](https://ubuntu.com/server/docs/nvidia-drivers-installation) to install NVIDIA drivers in the section named “Check the available drivers for your hardware”.   
2. Note: make sure your driver installation is the package name with no trailing notations after the version number. For instance, only install `nvidia-driver-xxx`, not `nvidia-driver-xxx-open`.

```
$ nvidia-smi
Tue Jun 18 09:18:44 2024
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 555.52.01              Driver Version: 555.99         CUDA Version: 12.5     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3090        On  |   00000000:0A:00.0  On |                  N/A |
|  0%   40C    P8             28W /  350W |    2424MiB /  24576MiB |      4%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A        29      G   /Xwayland                                   N/A      |
+-------
```

### WSL2

LEIP SDK runs on Linux. WSL2 is a good candidate, as it’s effectively a well integrated Linux VM on Windows.

* To install WSL2, [refer to this documentation](https://learn.microsoft.com/en-us/windows/ai/directml/gpu-cuda-in-wsl).  
* You should also install NVIDIA’s CUDA drivers for WSL2. The easiest way to accomplish this is to install CUDA, which will install the drivers themselves as a dependency.  
  * [Click this link](https://developer.nvidia.com/cuda-downloads?target\_os=Linux\&target\_arch=x86\_64\&Distribution=WSL-Ubuntu\&target\_version=2.0\&target\_type=deb\_network) to be directed to the installation instructions. We recommend the `deb (network)` instructions.  
* Once you install the GPU drivers with WSL2, you will be able to check if the GPU is available by typing the command `nvidia-smi` into the terminal. It should look something similar to the output below.

```
$ nvidia-smi
Tue Jun 18 09:18:44 2024
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 555.52.01              Driver Version: 555.99         CUDA Version: 12.5     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3090        On  |   00000000:0A:00.0  On |                  N/A |
|  0%   40C    P8             28W /  350W |    2424MiB /  24576MiB |      4%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A        29      G   /Xwayland                                   N/A      |
+-----------------------------------------------------------------------------------------+
```

# Step 2: Installing Docker

### Ubuntu

1. Refer to [this section of the Docker documentation ("Install using the apt repository")](https://docs.docker.com/engine/install/ubuntu/\#install-using-the-repository) to install Docker via `apt`.  
   1. You should now be able to use the `docker` command, but you will need to type `sudo` every time. To use `docker` without typing `sudo`, [follow this specific section in the Docker documentation (“Manager Docker as a non-root user)](https://docs.docker.com/engine/install/linux-postinstall/\#manage-docker-as-a-non-root-user).  
1. Enable the GPU for usage inside Docker. To do this, install `nvidia-container-runtime` by following [this specific section](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html\#installing-with-apt) (“Installing with Apt”).  
1. Now, we need to set Docker to leverage the NVIDIA runtime. Following **only the first two steps** [in this specific section (“Configuring Docker)](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html\#configuring-docker).  
1. You should now be able to use your GPU inside Docker. You should be able to run this test to verify:

```
$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark

Run "nbody -benchmark [-numbodies=<numBodies>]" to measure performance.
        -fullscreen       (run n-body simulation in fullscreen mode)
        -fp64             (use double precision floating point values for simulation)
        -hostmem          (stores simulation data in host memory)
        -benchmark        (run benchmark to measure performance)
        -numbodies=<N>    (number of bodies (>= 1) to run in simulation)
        -device=<d>       (where d=0,1,2.... for the CUDA device to use)
        -numdevices=<i>   (where i=(number of CUDA devices > 0) to use for simulation)
        -compare          (compares simulation results running once on the default GPU and once on the CPU)
        -cpu              (run n-body simulation on the CPU)
        -tipsy=<file.bin> (load a tipsy model file for simulation)

NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.

> Windowed mode
> Simulation data stored in video memory
> Single precision floating point simulation
> 1 Devices used for simulation
GPU Device 0: "Turing" with compute capability 7.5

> Compute 7.5 CUDA device: [NVIDIA GeForce RTX 2060]
30720 bodies, total time for 10 iterations: 69.751 ms
= 135.299 billion interactions per second
= 2705.976 single-precision GFLOP/s at 20 flops per interaction
```

### WSL2

The easiest way to accomplish this is to [install Docker Desktop](https://docs.docker.com/desktop/install/windows-install/), which will enable Docker automatically with CUDA in WSL2 upon installing CUDA \+ NVIDIA Drivers.
