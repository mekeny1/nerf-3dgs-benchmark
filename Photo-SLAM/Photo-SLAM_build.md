# Photo-SLAM_build.md

## Photo-SLAM

### 基础

#### docker build

**Photo-SLAM\.devcontainer**：修改部分配置

将所需下载资源提前下载，并通过 **WinSCP** 链接服务器放于 **nerf-3dgs-benchmark** 的 **Photo-SLAM** 目录（容器目录 **/workspace** 对应到宿主机中的目录）

**vsc+docker插件** build docker容器

#### 预处理

**cmake**：

```bash
mv cmake-3.22.1-linux-x86_64.sh / && \
		    chmod +x /cmake-3.22.1-linux-x86_64.sh && \
		    /cmake-3.22.1-linux-x86_64.sh --skip-license --prefix=/usr/local
```



**opencv**：

```bash
mkdir /opencv && \
    mv opencv-4.8.0.zip /opencv && \
  	  mv opencv_contrib-4.8.0.zip /opencv && \
  	  cd /opencv && \
  	  unzip opencv-4.8.0.zip && \
  	  unzip opencv_contrib-4.8.0.zip && \
  	  rm opencv-4.8.0.zip && rm opencv_contrib-4.8.0.zip
```



**opencv build**（编译opencv时会额外下载一些包，易受网络质量影响，等最终编译结果再做处理）：

```bash
mkdir /opencv/opencv-4.8.0/build && cd /opencv/opencv-4.8.0/build && \
		    cmake -DCMAKE_BUILD_TYPE=RELEASE \
          -DWITH_CUDA=ON \
          -DWITH_CUDNN=ON \
          -DOPENCV_DNN_CUDA=ON \
          -DWITH_NVCUVID=ON \
          -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-11.8 \
          -DOPENCV_EXTRA_MODULES_PATH=/opencv/opencv_contrib-4.8.0/modules \
          -DBUILD_TIFF=ON \
          -DBUILD_ZLIB=ON \
          -DBUILD_JASPER=ON \
          -DBUILD_JPEG=ON \
          -DWITH_FFMPEG=ON \
          .. && \
    make -j$(nproc) && \
    make install && \
    ldconfig
```



**libtorch**：

```bash
mv libtorch-cu118.zip / && cd / && \
    unzip libtorch-cu118.zip && rm libtorch-cu118.zip
```



#### Photo-SLAM构建

**添加环境变量**：

```bash
export DISPLAY_EXPORT="export DISPLAY=:0"
```



**clone**（置于 **nerf-3dgs-benchmark** 的 **Photo-SLAM**）：

```bash
git clone --recursive https://github.com/iis-esslingen/Photo-SLAM.git
```



**Photo-SLAM编译**：

```bash
cd /workspace/Photo-SLAM
chmod +x ./build.sh
./build.sh
```



### issues

### custom datasets

