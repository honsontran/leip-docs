**Problem**

If you are trying to optimize a model on older (pre-Volta/Turing), you may encounter an error similar to this:

 `/latentai# leip pipeline --config_path /latentai/recipes/yolov5_S_RT/pipeline_x86_64_cuda.yaml  Pipeline Yolov5_S_RT, flow Float32, step 1: compile... :white_check_mark:  Pipeline Yolov5_S_RT, flow Int8, step 1: optimize... :x:  Summary:  ------------------------------------------------------------------------------  Flow Float32      1 compile: :white_check_mark:  Flow Int8      1 optimize: :x: TVMError:  Check failed: ret == 0 (-1 vs. 0) : CUDAError: cuModuleLoadData(&(module_[device_id]), data_.c_str()) failed with error: CUDA_ERROR_INVALID_PTX  ------------------------------------------------------------------------------  Pipeline completed with failed flows.`

The problem here is that the cross compilation settings in the example recipe are configured to match the architecture of the Xavier AGX and NX devices (sm_70). LEIP Optimize uses the GPU of the host, and if you are using a Pascal era card, you will need to modify the configuration to match the architecture of that card.

**Solution**

1. Find the pipeline configuration file that you are using to compile and optimize your model. For the example above, the Yolov5 Small model is being used, with the target device being x86_64 with CUDA.
2. The configuration file for that configuration is included in `/latentai/recipes/yolov5_S_RT/pipeline_x86_64_cuda.yaml`
3. Edit the file you are using to change each instance of `sm_70` to
    1. `sm_60` (for Pascal architecture GPUs); or
    2. `sm_50` (for Maxwell architecture GPUs)
4. Re-run LEIP Pipeline.

**Versions**

This cross compilation result is a known issue starting with Recipes release in LEIP 2.4.

---------------
**

## docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]]

$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark

docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].

If you face this error. You have to install nvidia-container-runtime as mentioned in the steps above.**