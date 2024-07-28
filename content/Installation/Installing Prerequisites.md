---
tags:
  - installation
  - getting-started
  - tutorials
custom-width: .nan
---
# Prerequisites

> [!WARNING] Warning
> For Windows users, WSL2 is needed to run [[What is LEIP?|LEIP SDK]]. We currently do not support native Windows.

As a general supportability statement, any OS that has Docker installed with access to a CUDA-enabled GPU can utilize [[What is LEIP?|LEIP SDK]].

For our testing, we have used:
* Linux-based system (Ubuntu 20.04 or 22.04)  
* NVIDIA GPU (from CUDA 10 to CUDA 12).  
* Docker 1.19 or greater
## Useful Prerequisite Links
### Ubuntu
* [Create an Ubuntu Installation USB & Install Ubuntu](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows/#1-overview)
	* Note: [[#Step 1 Installing NVIDIA Drivers]] can be achieved by simply enabling the installation of third-party drivers, as this will automatically install NVIDIA drivers. [[ubuntu-install-third-party.png|Click here]] to view where this can be checked off.
### Windows (WSL2)
* [How to Install WSL2](https://learn.microsoft.com/en-us/windows/ai/directml/gpu-cuda-in-wsl)
	* If you're running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11, the easiest way to install WSL2 is by opening a PowerShell **as administrator** and type `wsl --install`. This will default to the Ubuntu distro.
	* You can change the WSL distro choice by typing `wsl -l -o` to view the `list` of available distros `online`, then typing `wsl --install -d <Distribution Name>` to install the chosen distro. 
	* For the manual install refer to [this page](https://learn.microsoft.com/en-us/windows/wsl/install-manual).
# Step 1: Installing NVIDIA Drivers

> [!WARNING]  Skip this section if...
>You can skip this step if your environment has a CUDA-enabled GPU installed properly.
>
>Simply type `nvidia-smi` into a terminal to verify. You should be able to see [[#Successful Output (Step 1)|this output]] if successful.
## Ubuntu (and other Linux-Based Distros)
1. Based on your Linux distro, `update` your package index files. For Ubuntu, that would be `sudo apt update`
2. Simply [go to this link](https://developer.nvidia.com/cuda-downloads), select your architecture, distro, the latest CUDA version, and select "deb (network)."
3. Follow the "Driver Installer" instructions.
## Windows (WSL2)
1. Go to this [link](https://www.nvidia.com/download/index.aspx).
2. Fill out your OS and GPU details, click search.
3. Click download.
4. Run the `.exe` and install 
## Successful Output (Step 1)

> [!NOTE] Note
> You should also take note of the `CUDA Version` on the top right corner of the output. This version does ***not*** represent your CUDA version installed on the system, but is listed to state what CUDA version your drivers can support up to.

To verify a successful installation, simply type `nvidia-smi` into your terminal. You should see a similar output below.
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
# Step 2: Installing Docker

> [!WARNING]  Skip this section if...
> If you are able to type `docker` in the terminal and return back [[#Successful Output (Step 2)|this output]], you have Docker installed.
## Ubuntu
1. Refer to [this link](https://docs.docker.com/engine/install/ubuntu/\#install-using-the-repository) (Install using the apt repository) to install Docker via `apt`.  
1. Enable the GPU for usage inside Docker. To do this, install `nvidia-container-runtime` by following [this specific section](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html\#installing-with-apt) (“Installing with Apt”).  
1. Now, we need to set Docker to leverage the NVIDIA runtime. Following **only the first two steps** [in this specific section (“Configuring Docker)](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html\#configuring-docker).  
## Other Linux Distros
It is possible to run containers with other Docker alternatives, such as `containerd`, but installation is currently not supported by us.
## Windows (WSL2)
1. The easiest way to accomplish this is to [install Docker Desktop](https://docs.docker.com/desktop/install/windows-install/), which will enable Docker automatically with your NVIDIA GPU.

## Successful Output (Step 2)

> [!TIP] Tip
> If you cannot use `docker` without `sudo`, [follow these instructions](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) (Manage Docker as a non-root user) and restart your computer to allow your `user` to use `docker` without `sudo` privileges.

Type `docker` in your terminal and verify if you can see a similar output as the one below.

```
$ docker

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
	...

Management Commands:
	...

Swarm Commands:
  swarm       Manage Swarm

Commands:
	...

Global Options:
	...

Run 'docker COMMAND --help' for more information on a command.[[]]

For more help on how to use Docker, head to https://docs.docker.com/go/guides/
```
# Step 3: Enable GPU Usage in Docker
To enable Docker to use NVIDIA GPUs, we need to install `nvidia-container-toolkit`.
1. Visit the "Installation" section of [this link](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)
2. Follow the "Configuration" section [in the same link](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#configuring-docker). You do not have to follow the "Rootless Mode," only the first two steps.
# Step 4: Verify GPU Usage by Docker
The easiest test to verify if you have GPU access in a Docker container is by running the command below:
```
docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```
### Successful Output
```
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
# Step 5: Install LEIP
Refer to [[Installing LEIP SDK]].