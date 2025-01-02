
> 将市面上几乎所有的LLM部署方案都测试了一遍之后（ollama, lm-studio, vllm, huggingface, lmdeploy），发现只有llama.cpp的推理速度符合企业要求。只是安装困难，遂记录于此。

## linux

### 安装nvidia驱动

### 安装cuda-toolkit

### gcc 与 cmake 版本

### 编译 llama.cpp CUDA加速

## windows

### 安装 vs
注意不是vs-code
安装勾选项：

### 编译 llama.cpp
自行编译各种报错，遂通过llamacpp-python进行自动化编译。CUDA加速通过环境变量即可。