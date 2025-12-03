# MonoGS_build.md

## MonoGS

### 基础

需要在构建容器前clone到nerf-3dgs-benchmark的MonoGS目录下

```bash
git clone --recursive https://github.com/iis-esslingen/MonoGS.git
```



**创建conda环境**：

```shell
cd MonoGS
mamba env create -f environment.yml -y
mamba activate MonoGS
```



**编译安装额外依赖**：

```bash
pip install submodules/diff-gaussian-rasterization
pip install submodules/simple-knn
```

