# Splat-SLAM_build

## Splat-SLAM

### 基础

#### docker build

（forked，下载到本地，更新后push，服务器再pull进行更新）`nerf-3dgs-benchmark\Splat-SLAM\.devcontainer`：修改部分配置

将所需下载资源提前下载到本地，并通过 **WinSCP** 软件链接到服务器，放于 `nerf-3dgs-benchmark\Splat-SLAM`（容器目录 **/workspace** 对应到服务器中的目录）

**clone**（服务器，容器的话是root权限）：

```bash
git clone --recursive https://github.com/google-research/Splat-SLAM.git
```



**vsc+docker插件**：工作空间中build docker

#### 预处理



#### Splat-SLAM构建

**创建 conda 环境**：该镜像自带conda，使用base环境即可，激活：

```bash
conda init bash
```



```bash
DISPLAY_EXPORT="export DISPLAY=:0"
cd /workspace/Splat-SLAM
```



**修改源代码文件**：

```bash
sed -i 's/p_view\.z <= 0\.2f/p_view\.z <= 0\.001f/' /workspace/Splat-SLAM/thirdparty/diff-gaussian-rasterization-w-pose/cuda_rasterizer/auxiliary.h
```



**安装额外依赖**：

此处有个点需要注意，就是pip的构建：
>有 `pyproject.toml`：肯定 PEP 517 + build isolation
>
>只有 `setup.py`：
>
>- 老 pip：legacy build，不隔离，直接跑 `python setup.py ...`
>- 新 pip：经常强行套一层 PEP 517，走 `setuptools.build_meta` + build isolation

所以 `setup.py` 的最好使用旧版本pip，如"pip==23.2.1" "setuptools<70"

```bash
pip install --no-cache-dir -e thirdparty/lietorch/ \
                              thirdparty/diff-gaussian-rasterization-w-pose/ \
                              thirdparty/simple-knn/ \
                              thirdparty/evaluate_3d_reconstruction_lib/ && \
    pip install --no-cache-dir -e . && \
    pip install --no-cache-dir -r requirements.txt && \
    pip install --no-cache-dir pytorch-lightning==1.9 --no-deps
```



### issues

### custom datasets
