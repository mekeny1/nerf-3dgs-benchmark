# GO-SLAM_build

## GO-SLAM

### 基础

#### docker build

（forked，下载到本地，更新后 `push`，服务器再 `pull` 进行更新）`nerf-3dgs-benchmark\GO-SLAM\.devcontainer`：修改部分配置

将所需下载资源提前下载到本地，并通过 **WinSCP** 软件链接到服务器，放于 `nerf-3dgs-benchmark\GO-SLAM`（容器目录 **/workspace** 对应到服务器中的目录）

**clone**（服务器上clone，容器的话是root权限不方便）：

```bash
git clone --recursive https://github.com/iis-esslingen/GO-SLAM.git
```



**vsc+docker插件**：工作空间中build docker

#### GO-SLAM构建

```bash
DISPLAY_EXPORT="export DISPLAY=:0"
```



**conda环境构建**：

```bash
cd cd /workspace/GO-SLAM
mamba env create -f environment.yaml -y
mamba activate go-slam
```



**额外依赖安装**：

```bash
pip install git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
pip install evo --upgrade --no-binary evo
python setup.py install
```



### issues

### custom datasets
