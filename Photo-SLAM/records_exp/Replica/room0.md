### 1）room0
#### ①train
```shell
./bin/replica_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/Replica/room0.yaml \
    ./cfg/gaussian_mapper/RGB-D/Replica/replica_rgbd.yaml \
    ./datasets/Replica/room0/ \
    ./output/Replica/room0/
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
Loading settings from ./cfg/ORB_SLAM3/RGB-D/Replica/room0.yaml
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
	-Camera 1 parameters (Pinhole): [ 600 600 599.5 339.5 ]
	-Camera 1 distortion parameters: [  0.000238406 -0.000314798 -7.39231e-05 -2.7716e-05 0 ]
	-Original image size: [ 1200 , 680 ]
	-Current image size: [ 1200 , 680 ]
	-Sequence FPS: 30
	-RGB-D depth map factor: 6553.5
	-Features per image: 1600
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
[Gaussian Mapper]Reading parameters from "./cfg/gaussian_mapper/RGB-D/Replica/replica_rgbd.yaml"
[ImGuiViewer]Reading parameters from "./cfg/gaussian_mapper/RGB-D/Replica/replica_rgbd.yaml"

-------
Start processing sequence ...
Images in the sequence: 2000

First KF:0; Map init KF:0
New Map created with 1609 points
*Loop detected
Local Mapping STOP
Loop: mpCurrentKF -> 156
Loop: number of connected KFs -> 57
Local Mapping RELEASE
[Gaussian Mapper]Loop Closure Detected.
Local Mapping STOP
Local Mapping RELEASE
Shutdown

Saving camera trajectory to ./output/Replica/room0/CameraTrajectory_TUM.txt ...

Saving keyframe trajectory to ./output/Replica/room0/KeyFrameTrajectory_TUM.txt ...

Saving trajectory to ./output/Replica/room0/CameraTrajectory_EuRoC.txt ...
There are 1 maps in the atlas
  Map 0 has 158 KFs

End of saving trajectory to ./output/Replica/room0/CameraTrajectory_EuRoC.txt ...

Saving keyframe trajectory to ./output/Replica/room0/KeyFrameTrajectory_EuRoC.txt ...

Saving camera trajectory to ./output/Replica/room0/CameraTrajectory_KITTI.txt ...
```

#### ②eval
- onekey.py->gt_dataset保留要运行的数据集即可，单数据集多场景（推荐），路径具体到数据集（ **../output/tum_rgbd_0/** ）；也可所有数据集场景一起评估，路径为 **../output/** 
- onekey.py->gt_dataset中，数据集路径（如 **tum_rgbd** ）不可带 **/** ，否则路径识别出成 **/** 下
```shell
python onekey.py -d ../datasets/ -r ../output/
```
- eval log
```shell
rendering room0:   0%|                                                             | 0/2000 [00:00<?, ?it/s]Setting up [LPIPS] perceptual loss: trunk [alex], v[0.1], spatial [off]
Loading model from: /root/miniconda3/lib/python3.10/site-packages/lpips/weights/v0.1/alex.pth
rendering room0: 100%|██████████████████████████████████████████████████| 2000/2000 [01:19<00:00, 25.03it/s]
APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.011669
      mean	0.004896
    median	0.004798
       min	0.000694
      rmse	0.005181
       sse	0.053696
       std	0.001695
```
