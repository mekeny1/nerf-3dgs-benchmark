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



**额外依赖安装**：

```bash
pip install thirdparty/evaluate_3d_reconstruction_lib
python setup.py install
```



#### 编译open3d

```bash
cd /workspace/GlORIE-SLAM/thirdparty && mamba activate glorie-slam
```



```bash
git clone --recursive https://github.com/isl-org/Open3D.git
cd Open3D
git checkout v0.16.0
git status
git describe --tags
mkdir build && cd build
```



编译：

```bash
PYTHON_EXEC=$(which python)

cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DBUILD_SHARED_LIBS=ON \
  -DENABLE_HEADLESS_RENDERING=ON \
  -DBUILD_GUI=OFF \
  -DUSE_SYSTEM_GLEW=OFF \
  -DUSE_SYSTEM_GLFW=OFF \
  -DBUILD_WEBRTC=OFF \
  -DBUILD_EXAMPLES=OFF \
  -DBUILD_TESTS=OFF \
  -DBUILD_PYTHON_MODULE=ON \
  -DPYTHON_EXECUTABLE=${PYTHON_EXEC}
```



安装：

```bash
# 仍在 Open3D/build 目录
make -j$(nproc)

# 回到 Open3D 根目录，安装 Python 包到当前环境
cd ..
python -m pip install .
```



测试：

```bash
python -c "import open3d as o3d; print(o3d.__version__)"
```



### issues

### custom datasets
