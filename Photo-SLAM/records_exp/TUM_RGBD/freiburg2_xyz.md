### 1）freiburg2_xyz
#### ①train
```shell
./bin/tum_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg2_xyz.yaml \
    ./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml \
    ./datasets/TUM_RGBD/rgbd_dataset_freiburg2_xyz/ \
    ./cfg/ORB_SLAM3/RGB-D/TUM/associations/tum_freiburg2_xyz.txt \
    ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/
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
Loading settings from ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg2_xyz.yaml
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
	-Camera 1 parameters (Pinhole): [ 520.909 521.007 325.141 249.702 ]
	-Camera 1 distortion parameters: [  0.231222 -0.784899 -0.003257 -0.000105 0.917205 ]
	-Original image size: [ 640 , 480 ]
	-Current image size: [ 640 , 480 ]
	-Sequence FPS: 30
	-RGB-D depth map factor: 5208
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
Images in the sequence: 3615

First KF:0; Map init KF:0
New Map created with 1729 points
Shutdown

Saving camera trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/CameraTrajectory_TUM.txt ...

Saving keyframe trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/KeyFrameTrajectory_TUM.txt ...

Saving trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/CameraTrajectory_EuRoC.txt ...
There are 1 maps in the atlas
  Map 0 has 46 KFs

End of saving trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/CameraTrajectory_EuRoC.txt ...

Saving keyframe trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/KeyFrameTrajectory_EuRoC.txt ...

Saving camera trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg2_xyz/CameraTrajectory_KITTI.txt ...
```

#### ②eval
- onekey.py->gt_dataset保留要运行的数据集即可，单数据集多场景（推荐），路径具体到数据集（ **../output/tum_rgbd_0/** ）；也可所有数据集场景一起评估，路径为 **../output/** 
- onekey.py->gt_dataset中，数据集路径（如 **tum_rgbd** ）不可带 **/** ，否则路径识别出成 **/** 下
```shell
python onekey.py -d ../datasets/ -r ../output/
```
- eval log
```shell
rendering rgbd_dataset_freiburg2_xyz:   0%|                                        | 0/3615 [00:00<?, ?it/s]Setting up [LPIPS] perceptual loss: trunk [alex], v[0.1], spatial [off]
Loading model from: /root/miniconda3/lib/python3.10/site-packages/lpips/weights/v0.1/alex.pth
rendering rgbd_dataset_freiburg2_xyz: 100%|█████████████████████████████| 3615/3615 [03:42<00:00, 16.25it/s]
APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.011091
      mean	0.003079
    median	0.002822
       min	0.000187
      rmse	0.003510
       sse	0.044550
       std	0.001687
```
