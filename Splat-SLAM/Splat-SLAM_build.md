# Splat-SLAM_build

## Splat-SLAM

### 基础

需要在构建容器前clone到nerf-3dgs-benchmark的Splat-SLAM目录下

```bash
git clone --recursive https://github.com/google-research/Splat-SLAM.git
```



### 容器创建后

**创建conda环境**：不需要，官方甚至没有用到conda命令，用系统自带的Python即可

```bash
DISPLAY_EXPORT="export DISPLAY=:0"
```



```bash
cd /workspace/Splat-SLAM
```



**修改源代码文件**：

```bash
sed -i 's/p_view\.z <= 0\.2f/p_view\.z <= 0\.001f/' /workspace/Splat-SLAM/thirdparty/diff-gaussian-rasterization-w-pose/cuda_rasterizer/auxiliary.h
```



**按照额外依赖**：

```bash
# 安装第三方库（可编辑模式）
pip install --no-cache-dir -e thirdparty/lietorch/
pip install --no-cache-dir -e thirdparty/diff-gaussian-rasterization-w-pose/
pip install --no-cache-dir -e thirdparty/simple-knn/
pip install --no-cache-dir -e thirdparty/evaluate_3d_reconstruction_lib/

# 安装主项目（可编辑模式）
pip install --no-cache-dir -e .

# 安装 requirements.txt 中的依赖
pip install --no-cache-dir -r requirements.txt

# 安装 pytorch-lightning（不安装依赖）
pip install --no-cache-dir pytorch-lightning==1.9 --no-deps
```

