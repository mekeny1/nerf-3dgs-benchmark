# MonoGS_build.md

## MonoGS

### 基础

```bash
git clone --recursive https://github.com/iis-esslingen/MonoGS.git
cd MonoGS
```



**可将 "torchaudio"注释掉**：

```shell
mamba env create -f environment.yml -y
mamba activate MonoGS
```



**编译安装额外依赖**：

```bash
pip install submodules/diff-gaussian-rasterization
pip install submodules/simple-knn
```

