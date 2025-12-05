# Orbeez-SLAM_build

## Orbeez-SLAM

### 基础

#### docker build

（forked，下载到本地，更新后 `push`，服务器再 `pull` 进行更新）`nerf-3dgs-benchmark\Orbeez-SLAM\.devcontainer`：修改部分配置

将所需下载资源提前下载到本地，并通过 **WinSCP** 软件链接到服务器，放于 `nerf-3dgs-benchmark\Orbeez-SLAM`（容器目录 **/workspace** 对应到服务器中的目录）

**clone**（服务器上clone，容器的话是root权限不方便）：

```bash
git clone --recursive https://github.com/iis-esslingen/Orbeez-SLAM.git
```



**vsc+docker插件**：工作空间中build docker



```bash
ssh -R 17890:127.0.0.1:7897 ubuntu@117.50.33.109
```



```bash
export http_proxy=http://127.0.0.1:17890 && \
    export https_proxy=http://127.0.0.1:17890
```



#### Orbeez-SLAM构建





### issues

### custom datasets
