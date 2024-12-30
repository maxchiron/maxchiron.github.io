## Ubuntu24.04 LTS 默认为gcc14，若要安装并使用gcc13：

安装 GCC 13 并保留 GCC 14 可以给你灵活性，同时确保你的系统稳定。以下是在基于 Debian 的系统（如 Ubuntu）上安装 GCC 13 并设置默认版本的步骤。

### 步骤 1: 安装 GCC 13
首先，你需要安装 GCC 13。你可以通过终端使用以下命令来安装它：

```bash
sudo apt update
sudo apt install gcc-13 g++-13
```

### 步骤 2: 配置 `update-alternatives`
安装完成后，你可以使用 `update-alternatives` 命令来管理系统中的多个 GCC 版本。这允许你在不同版本之间轻松切换。

首先，设置 GCC 和 G++ 的替代配置：

```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-14 40 --slave /usr/bin/g++ g++ /usr/bin/g++-14
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-13 60 --slave /usr/bin/g++ g++ /usr/bin/g++-13
```

这里，`60` 和 `40` 是优先级。优先级更高的版本将成为默认版本。根据上面的设置，GCC 13 将被设置为默认版本。

### 步骤 3: 切换 GCC 版本
如果你需要切换到不同的 GCC 版本，你可以使用以下命令：

```bash
sudo update-alternatives --config gcc
```

这个命令将列出所有安装的 GCC 版本，并让你选择要使用的版本。

### 步骤 4: 验证安装
安装并配置完成后，你可以通过检查版本号来验证当前使用的 GCC 版本：

```bash
gcc --version
```

这应该显示 GCC 13 的相关信息，表明你已成功切换到 GCC 13。

完成这些步骤后，你的系统将配置好 GCC 13 作为默认的编译器，同时保留了 GCC 14，以便在需要时使用。这将帮助你解决任何与 CUDA 兼容性相关的问题，同时保持对最新编译器特性的访问。