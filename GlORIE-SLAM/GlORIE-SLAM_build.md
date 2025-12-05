# GlORIE-SLAM_build

## GlORIE-SLAM

### 基础

#### docker build

（forked，下载到本地，更新后 `push`，服务器再 `pull` 进行更新）`nerf-3dgs-benchmark\GlORIE-SLAM\.devcontainer`：修改部分配置

将所需下载资源提前下载到本地，并通过 **WinSCP** 软件链接到服务器，放于 `nerf-3dgs-benchmark\GlORIE-SLAM`（容器目录 **/workspace** 对应到服务器中的目录）

**clone**（服务器上clone，容器的话是root权限不方便）：

```bash
git clone --recursive https://github.com/iis-esslingen/GlORIE-SLAM.git
```



**open3d0.16.0**：clone时一定不能加 `--recursive`

```bash
cd /workspace/GlORIE-SLAM/thirdparty && \
    git clone https://github.com/isl-org/Open3D.git && \
    cd Open3D && \
    git checkout v0.16.0 && \
    git submodule update --init --recursive
```



**vsc+docker插件**：工作空间中build docker

#### GO-GlORIE-SLAM构建

```bash
DISPLAY_EXPORT="export DISPLAY=:0"
```



**conda环境构建**：

```bash
cd /workspace/GlORIE-SLAM && \
    mamba env create -f glorie_env.yaml -y && \
    mamba activate glorie-slam
```



#### open3d编译安装

只要网络挂了本地的代理，就不用太多问题

**open3d相关依赖**：若已经处于root权限，需提前注释掉 **util/install_deps_ubuntu.sh** 中的 sudo

```bash
cd thirdparty/Open3D/ && bash util/install_deps_ubuntu.sh
```



**Python环境配置**：

```bash
pip install pybind11 && mamba install cmake=3.22 -y
```



```bash
cd /workspace/GlORIE-SLAM/thirdparty/Open3D && \
    mkdir build && cd build
```



**CMake 编译配置**：

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_GUI=OFF \
    -DBUILD_WEBRTC=OFF \
    -DENABLE_HEADLESS_RENDERING=ON \
    -DBUILD_FILAMENT_GOOGLE_TESTS=OFF \
    -DUSE_SYSTEM_GLFW=OFF \
    -DBUILD_PYTHON_MODULE=ON \
    -DPython3_EXECUTABLE=$(which python)
```



**编译与安装**：

```bash
make -j$(nproc)
```



编译 Python Wheel 包：

```bash
make install-pip-package
```



**测试**：

```bash
python -c "import open3d as o3d; print(f'Open3D Version: {o3d.__version__}')"
```



#### 额外依赖

```bash
cd /workspace/GlORIE-SLAM && \
    pip install thirdparty/evaluate_3d_reconstruction_lib
```



**剩余依赖**：

```bash
python setup.py install
```



### issues

### custom datasets
