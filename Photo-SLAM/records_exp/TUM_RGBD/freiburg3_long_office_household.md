### 1）freiburg3_long_office_household
#### ①train
```shell
./bin/tum_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg3_long_office_household.yaml \
    ./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml \
    ./datasets/tum_rgbd/rgbd_dataset_freiburg3_long_office_household/ \
    ./cfg/ORB_SLAM3/RGB-D/TUM/associations/tum_freiburg3_long_office_household.txt \
    ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/
    # no_viewer 
```
- train log
```shell
CUDA available! Training on GPU.

ORB-SLAM3 Copyright (C) 2017-2020 Carlos Campos, Richard Elvira, Juan J. Gómez, José M.M. Montiel and Juan D. Tardós, University of Zaragoza.
ORB-SLAM2 Copyright (C) 2014-2016 Raúl Mur-Artal, José M.M. Montiel and Juan D. Tardós, University of Zaragoza.
This program comes with ABSOLUTELY NO WARRANTY;
This is free software, and you are welcome to redistribute it
under certain conditions. See LICENSE.txt.

Input sensor was set to: RGB-D
Loading settings from ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg3_long_office_household.yaml
Camera1.k3 optional parameter does not exist...
	-Loaded camera 1
Camera.newHeight optional parameter does not exist...
Camera.newWidth optional parameter does not exist...
	-Loaded image info
	-Loaded RGB-D calibration
	-Loaded ORB settings
Viewer.imageViewScale optional parameter does not exist...
	-Loaded viewer settings
System.LoadAtlasFromFile optional parameter does not exist...
System.SaveAtlasToFile optional parameter does not exist...
	-Loaded Atlas settings
System.thFarPoints optional parameter does not exist...
	-Loaded misc parameters
----------------------------------
SLAM settings: 
	-Camera 1 parameters (Pinhole): [ 535.4 539.2 320.1 247.6 ]
	-Camera 1 distortion parameters: [  0 0 0 0 ]
	-Original image size: [ 640 , 480 ]
	-Current image size: [ 640 , 480 ]
	-Sequence FPS: 30
	-RGB-D depth map factor: 5000
	-Features per image: 2000
	-ORB scale factor: 1.2
	-ORB number of scales: 8
	-Initial FAST threshold: 20
	-Min FAST threshold: 7


Loading ORB Vocabulary. This could take a while...
Vocabulary loaded!

Initialization of Atlas from scratch 
Creation of new map with id: 0
Creation of new map with last KF id: 0
Seq. Name: 
There are 1 cameras in the atlas
Camera 0 is pinhole
[Gaussian Mapper]CUDA available! Training on GPU.
[Gaussian Mapper]Reading parameters from "./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml"
[ImGuiViewer]Reading parameters from "./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml"

-------
Start processing sequence ...
Images in the sequence: 2488

First KF:0; Map init KF:0
New Map created with 1782 points
*Loop detected
Local Mapping STOP
Loop: mpCurrentKF -> 233
Loop: number of connected KFs -> 37
Local Mapping RELEASE
[Gaussian Mapper]Loop Closure Detected.
Local Mapping STOP
Local Mapping RELEASE
Shutdown

Saving camera trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/CameraTrajectory_TUM.txt ...

Saving keyframe trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/KeyFrameTrajectory_TUM.txt ...

Saving trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/CameraTrajectory_EuRoC.txt ...
There are 1 maps in the atlas
  Map 0 has 253 KFs

End of saving trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/CameraTrajectory_EuRoC.txt ...

Saving keyframe trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/KeyFrameTrajectory_EuRoC.txt ...

Saving camera trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg3_long_office_household/CameraTrajectory_KITTI.txt ...
(base) root@6441dfb81b1f:/app# ./bin/tum_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg1_360.yaml \
    ./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml \
    ./datasets/tum_rgbd/rgbd_dataset_freiburg1_360/ \
    ./cfg/ORB_SLAM3/RGB-D/TUM/associations/fr1_360.txt \
    ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/
CUDA available! Training on GPU.

ORB-SLAM3 Copyright (C) 2017-2020 Carlos Campos, Richard Elvira, Juan J. Gómez, José M.M. Montiel and Juan D. Tardós, University of Zaragoza.
ORB-SLAM2 Copyright (C) 2014-2016 Raúl Mur-Artal, José M.M. Montiel and Juan D. Tardós, University of Zaragoza.
This program comes with ABSOLUTELY NO WARRANTY;
This is free software, and you are welcome to redistribute it
under certain conditions. See LICENSE.txt.

Input sensor was set to: RGB-D
Loading settings from ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg1_360.yaml
	-Loaded camera 1
Camera.newHeight optional parameter does not exist...
Camera.newWidth optional parameter does not exist...
	-Loaded image info
	-Loaded RGB-D calibration
	-Loaded ORB settings
Viewer.imageViewScale optional parameter does not exist...
	-Loaded viewer settings
System.LoadAtlasFromFile optional parameter does not exist...
System.SaveAtlasToFile optional parameter does not exist...
	-Loaded Atlas settings
System.thFarPoints optional parameter does not exist...
	-Loaded misc parameters
----------------------------------
SLAM settings: 
	-Camera 1 parameters (Pinhole): [ 517.306 516.469 318.643 255.314 ]
	-Camera 1 distortion parameters: [  0.262383 -0.953104 -0.005358 0.002628 1.16331 ]
	-Original image size: [ 640 , 480 ]
	-Current image size: [ 640 , 480 ]
	-Sequence FPS: 30
	-RGB-D depth map factor: 5000
	-Features per image: 1200
	-ORB scale factor: 1.2
	-ORB number of scales: 8
	-Initial FAST threshold: 20
	-Min FAST threshold: 7


Loading ORB Vocabulary. This could take a while...
Vocabulary loaded!

Initialization of Atlas from scratch 
Creation of new map with id: 0
Creation of new map with last KF id: 0
Seq. Name: 
There are 1 cameras in the atlas
Camera 0 is pinhole
[Gaussian Mapper]CUDA available! Training on GPU.
[Gaussian Mapper]Reading parameters from "./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml"
[ImGuiViewer]Reading parameters from "./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml"

-------
Start processing sequence ...
Images in the sequence: 744

First KF:0; Map init KF:0
New Map created with 1134 points
*Loop detected
Local Mapping STOP
Loop: mpCurrentKF -> 136
Loop: number of connected KFs -> 19
Local Mapping RELEASE
[Gaussian Mapper]Loop Closure Detected.
Local Mapping STOP
Local Mapping RELEASE
Shutdown

Saving camera trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/CameraTrajectory_TUM.txt ...

Saving keyframe trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/KeyFrameTrajectory_TUM.txt ...

Saving trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/CameraTrajectory_EuRoC.txt ...
There are 1 maps in the atlas
  Map 0 has 180 KFs

End of saving trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/CameraTrajectory_EuRoC.txt ...

Saving keyframe trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/KeyFrameTrajectory_EuRoC.txt ...

Saving camera trajectory to ./output/tum_rgbd_0/rgbd_dataset_freiburg1_360/CameraTrajectory_KITTI.txt ...
```

#### ②eval
- onekey.py->gt_dataset保留要运行的数据集即可，单数据集多场景（推荐），路径具体到数据集（ **../output/tum_rgbd_0/** ）；也可所有数据集场景一起评估，路径为 **../output/** 
- onekey.py->gt_dataset中，数据集路径（如 **tum_rgbd** ）不可带 **/** ，否则路径识别出成 **/** 下
```shell
python onekey.py -d ../datasets/ -r ../output/
```
- eval log
```shell
rendering rgbd_dataset_freiburg3_long_office_household:   0%|                      | 0/2488 [00:00<?, ?it/s]Setting up [LPIPS] perceptual loss: trunk [alex], v[0.1], spatial [off]
Loading model from: /root/miniconda3/lib/python3.10/site-packages/lpips/weights/v0.1/alex.pth
rendering rgbd_dataset_freiburg3_long_office_household: 100%|███████████| 2488/2488 [02:40<00:00, 15.47it/s]
APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.106615
      mean	0.015216
    median	0.012715
       min	0.000283
      rmse	0.020965
       sse	1.093525
       std	0.014422
```
