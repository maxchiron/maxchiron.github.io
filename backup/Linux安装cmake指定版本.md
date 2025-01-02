1. apt 卸载当前cmake
2. [https://cmake.org/files](https://cmake.org/files/) 选择版本，下载.sh自动安装脚本
3. 安装时应用 ` --prefix=/usr/local` 指定安装位置
4. 安装时按照提示，使用 `subdir` ，从而将cmake安装在 `/usr/local/cmake-xxx/` 下，方便区分版本和卸载
5. 安装提示添加环境变量。`export PATH="/usr/local/cmake-xxx/bin:$PATH"`
6. `cmake --version`