## 使用Dockerfile构建

### 创建镜像

- **.**  表示Dockerfile在当前目录

```shell
docker build -t photo-slam:latest .
```

### 创建容器photoslam

1. 在宿主机下载仓库代码，再挂载到容器；在容器内设定固定的工作目录；映射gui到宿主机启动

```shell
docker run -it --name photoslam \
  --gpus all \
  -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
  -e DISPLAY=$DISPLAY \
  -v $HOME/.Xauthority:/tmp/.Xauthority:ro \
  -e XAUTHORITY=/tmp/.Xauthority \
  -v ~/Desktop/rec/Photo-SLAM:/app \
  --workdir /app \
  photo-slam:latest
```

2. 退出再进入

```shell
xhost +local:

docker start photoslam

docker exec -it photoslam bash
```

### 编译

```shell
chmod +x ./build.sh
./build.sh
```

### 运行

```shell
./bin/tum_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg1_360.yaml \
    ./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml \
    ./datasets/tum_rgbd/rgbd_dataset_freiburg1_360/ \
    ./cfg/ORB_SLAM3/RGB-D/TUM/associations/fr1_360.txt \
    ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/
    # no_viewer 
```

> line1：可执行文件，对应源码位于 **./examples/**
> line3：相机模型、orb
> line4：姿态优化、建图
> line5：输入的数据集
> line6：rgb与depth图的配准文件
> line7：训练结果保存目录
>
### 创建conda环境

- 容器内安装miniconda

```shell
mkdir -p ~/miniconda3
# 提示网络问题则开启tun mode；最新版Miniconda3与torchvision==0.16.2不兼容（torchvision 0.16.2 would require python >=3.10,<3.11.0a0 *）
wget https://repo.anaconda.com/miniconda/Miniconda3-py310_25.1.1-2-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh

source ~/miniconda3/bin/activate
conda init --all
```

- 安装依赖

```shell
conda install pytorch==2.1.2 torchvision==0.16.2 pytorch-cuda=11.8 -c pytorch -c nvidia

# numpy下载1.x（2.x报错：AttributeError: `np.unicode_` was removed in the NumPy 2.0 release. Use `np.str_` instead.）
conda install opencv numpy=1.26.4
pip install evo scipy scikit-image lpips pillow tqdm plyfile pytorch_msssim
```

### 评估

1. 由于docker容器内生成的文件，宿主机需添加权限修改，则在宿主机clone仓库代码

```shell
git clone https://github.com/HuajianUP/Photo-SLAM-eval.git
```

- 注意事项
  - run.py将import numpy as np置于开头
  - onekey.py->gt_dataset保留要运行的数据集即可，单数据集多场景（推荐），路径具体到数据集（ **../output/tum_rgbd_0/** ）；也可所有数据集场景一起评估，路径为 **../output/**
  - onekey.py->gt_dataset中，数据集路径（如 **tum_rgbd** ）不可带 **/** ，否则路径识别出成 **/** 下
  - Copy TUM camera.yaml to the corresponding dataset path：Since images on some sequences of TUM dataset contain distortion, we need to undistort the ground truth images before evaluation. In addition, the file camera.yaml is used as an indicator in run.py.

 ```shell
	cp ./TUM/fr1/camera.yaml ../datasets/tum_rgbd/rgbd_dataset_freiburg1_desk
	cp ./TUM/fr2/camera.yaml ../datasets/tum_rgbd/rgbd_dataset_freiburg2_xyz
 ```

 	- onekey.py中的场景要与datasets里的一致，且不能出现除场景数据集文件夹的其他文件夹

- Install submodel for rendering

```shell
cd /app/Photo-SLAM-eval/
pip install submodules/simple-knn/ 
pip install submodules/diff-gaussian-rasterization/
```

- 运行

```shell
python onekey.py -d ../datasets/ -r ../output/
```

## .2 本地构建（失败）

### 准备cuda与torch

- 准备cuda与torch环境：使用C++的libtorch，或conda管理的pytorch（推荐）

```shell
# 在CMakeLists.txt中find_package(Torch REQUIRED)前添加一行
set(Torch_DIR /opt/miniconda3/envs/gslam/lib/python3.10/site-packages/torch/share/cmake/Torch)
```

### 安装opencv4.8.0

- 下载opencv及对应的opencv_contrib的压缩包，解压到同一目录下（/path/to/opencv）

> <https://github.com/opencv/opencv/archive/refs/tags/4.8.0.tar.gz>
> <https://github.com/opencv/opencv_contrib/archive/refs/tags/4.8.0.tar.gz>

- 编译opencv

```shell
cd /path/to/opencv-4.8.0/
mkdir build
cd build

# 注：给的cmake命令中要将cuda-11.8改为本地安装的cuda版本（如11.7），并设置opencv安装目录（/opt/安装第三方大型、独立的；/usr/local/安装本地编译或自行安装的，一般不属于系统的包管理）
cmake -DCMAKE_BUILD_TYPE=RELEASE \
      -DWITH_CUDA=ON \
      -DWITH_CUDNN=ON \
      -DOPENCV_DNN_CUDA=ON \
      -DWITH_NVCUVID=ON \
      -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-11.7 \
      -DOPENCV_EXTRA_MODULES_PATH="../../opencv_contrib-4.8.0/modules" \
      -DBUILD_TIFF=ON \
      -DBUILD_ZLIB=ON \
      -DBUILD_JASPER=ON \
      -DBUILD_CCALIB=ON \
      -DBUILD_JPEG=ON \
      -DWITH_FFMPEG=ON \
      -DCMAKE_INSTALL_PREFIX=/usr/local/opencv-4.8.0/ \
      ..

# Take a moment to check the cmake output, see if there are any packages needed by OpenCV but not installed on your device
make -j$(nproc)
# NOTE: We found that the compilation of OpenCV may stuck at 99%, this may be caused by the final linking process. We just waited for a while until it was completed and exited without errors.
```

- To install OpenCV into the system path

```shell
# 安装在指定的目录下（便于后期安装多版本或卸载）
sudo make install -DCMAKE_INSTALL_PREFIX=/usr/local/opencv-4.8.0/
```

### 安装Photo-SLAM

```shell
git clone https://github.com/HuajianUP/Photo-SLAM.git
cd Photo-SLAM/
# 修改build.sh，根据提示添加
# -DTorch_DIR=/opt/miniconda3/envs/photo-slam/lib/python3.10/site-packages/torch/share/cmake/Torch/
# -DOpenCV_DIR=/usr/local/opencv-4.8.0/lib/cmake/opencv4/
chmod +x ./build.sh
./build.sh
```
