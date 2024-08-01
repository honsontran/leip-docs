## Target Architecture Supportability

LEIP currently supports the following hardware:

| Hardware          | OS           | Additional requirements                    |
| ----------------- | ------------ | ------------------------------------------ |
| Raspberry Pi 4    | Debian 11    | Python 3.9                                 |
| AGX / NX (Xavier) | Ubuntu 20.04 | Jetpack 5.1.2                              |
| AGX (Orin)        | Ubuntu 20.04 | Jetpack 5.1.2                              |
| x86 CUDA          | Ubuntu 20.04 | CUDA 11.8, TensorRT 8.5, CuDNN 8, CuFFT 10 |
| x86 CUDA          | Ubuntu 20.04 | CUDA 12, TensorRT 8.6, CuDNN 8, CuFFT 11   |
| x86 CUDA          | Ubuntu 22.x  | CUDA 12, TensorRT 8.6, CuDNN 8, CuFFT 11   |

Additional hardware support will be added in future releases.