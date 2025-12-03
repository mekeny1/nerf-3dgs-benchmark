# ORB_SLAM3

https://fishros.org.cn/forum/topic/842/，适用于 ubuntu18.04/20.04

## as

### as

#### ros 一键安装

**安装 opencv，版本 3** 

```shell
wget http://fishros.com/install -O fishros && . fishros
```

#### c++编译工具

**ubuntu 默认版本即可** 

```shell
sudo apt update
sudo apt install git cmake gcc g++

```


#### EIGEN3 安装

```shell
sudo apt-get install libeigen3-dev

```
#### pangolin 安装

***https://github.com/stevenlovegrove/Pangolin*，下载 v0.6 的压缩包** 

1. 此前不适合（或编译失败）的版本卸载
```shell
cd Pangolin/build
make clean
sudo make uninstall  //卸载
sudo rm -r /usr/local/include/pangolin //删除残留文件
cd ../..
sudo rm -r Pangolin  //删除源代码

```




2. 依赖安装

```shell
sudo apt install libglew-dev libpython2.7-dev cmake pkg-config libegl1-mesa-dev libwayland-dev libxkbcommon-dev wayland-protocols ffmpeg libavcodec-dev libavutil-dev libavformat-dev libswscale-dev libavdevice-dev
```



3. Pangolin 安装

```shell
sudo apt install libgl1-mesa-dev
# cd Pangolin，进入源码文件夹
mkdir build
cd build
cmake ..
make
sudo make install

# 若以上代码报错，执行
sudo apt install libgl1-mesa-dev
sudo apt install pkg-config
sudo apt install libegl1-mesa-dev libwayland-dev libxkbcommon-dev wayland-protocols

```


#### opencv 安装

ros 一键安装（ros melodic）已经安装了 opencv3.2，不能再安装 4 版本的，opencv3 版和 4 版会冲突

```shell
# 查看 opencv 版本
pkg-config opencv --modversion

```
#### 6）ORB-SLAM3 安装
- https://github.com/UZ-SLAMLab/ORB_SLAM3.git， v1.0 与 0.4 皆可用（建议直接下这两个版本之一的压缩包），但 1.0 需要修改 CMakeList.txt 里有关 opencv 版本的内容
```shell
cd ORB_SLAM3
chmod +x build.sh
# 由于 orbslam3 的 v1.0 版本的 CMakeLists.txt 中要求 opencv 版本为 4.4，所以修改为以下内容。同样，如果系统安装的为 4.2 亦可改为：find_package(OpenCV 4.2)
find_package(OpenCV 3 REQUIRED)
# 回到终端执行，编译完后生成 c/cpp 代码的可执行文件
./build.sh

# 在 ubuntu 22.04 里面编译报错，需要 c++14 在主 CMakeLists.txt 加 add_compile_options(-std = c++14)，加上这行代码能通过编译，如下
add_compile_options(-std=c++14)
LIST(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)

```
#### 7）运行 rgbd 数据（以 tumrgbd 手持 slam 数据的 360 为例）
1. orbslam3 目录下创建 datasets/tum_rgbd，并将 360 数据解压放入

2. 下载官方的数据对齐脚本（https://svncvpr.in.tum.de/cvpr-ros-pkg/trunk/rgbd_benchmark/rgbd_benchmark_tools/src/rgbd_benchmark_tools/associate.py），放于 Examples/RGB-D/目录下，并修改代码 line86、87，如下

	> first_keys = list(first_list.keys())
	> second_keys = list(second_list.keys())
```shell
# conda 安装好 numpy（使用 python3）, 终端执行，生成匹配信息文件
python3 ./Examples/RGB-D/associate.py ./Datasets/tum_rgbd_slam/rgbd_dataset_freiburg1_360/rgb.txt ./Datasets/tum_rgbd_slam/rgbd_dataset_freiburg1_360/depth.txt >Datasets/tum_rgbd_slam/rgbd_dataset_freiburg1_360/associations.txt
```
3. 运行

```shell
./Examples/RGB-D/rgbd_tum ./Vocabulary/ORBvoc.txt ./Examples/RGB-D/TUM1.yaml ./Datasets/tum_rgbd_slam/rgbd_dataset_freiburg1_360/ ./Datasets/tum_rgbd_slam/rgbd_dataset_freiburg1_360/associations.txt

```
4. 运行结果（估计的位姿信息：时间戳+xyz 坐标+四元数）：median tracking time: 0.0131251，mean tracking time: 0.0134128；CameraTrajectory.txt，KeyFrameTrajectory.txt
