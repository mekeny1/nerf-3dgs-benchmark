### 1）freiburg1_room
#### ①train
```shell
./bin/tum_rgbd \
    ./ORB-SLAM3/Vocabulary/ORBvoc.txt \
    ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg1_room.yaml \
    ./cfg/gaussian_mapper/RGB-D/TUM/tum_rgbd.yaml \
    ./datasets/TUM_RGBD/rgbd_dataset_freiburg1_room/ \
    ./cfg/ORB_SLAM3/RGB-D/TUM/associations/fr1_room.txt \
    ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/
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
Loading settings from ./cfg/ORB_SLAM3/RGB-D/TUM/tum_freiburg1_room.yaml
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
Images in the sequence: 1352

First KF:0; Map init KF:0
New Map created with 991 points
*Loop detected
Local Mapping STOP
Loop: mpCurrentKF -> 197
Loop: number of connected KFs -> 6
Local Mapping RELEASE
[Gaussian Mapper]Loop Closure Detected.
Local Mapping STOP
Local Mapping RELEASE
Shutdown

Saving camera trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/CameraTrajectory_TUM.txt ...

Saving keyframe trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/KeyFrameTrajectory_TUM.txt ...

Saving trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/CameraTrajectory_EuRoC.txt ...
There are 1 maps in the atlas
  Map 0 has 252 KFs

End of saving trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/CameraTrajectory_EuRoC.txt ...

Saving keyframe trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/KeyFrameTrajectory_EuRoC.txt ...

Saving camera trajectory to ./output/TUM_RGBD/rgbd_dataset_freiburg1_room/CameraTrajectory_KITTI.txt ...
```

#### ②eval
- onekey.py->gt_dataset保留要运行的数据集即可，单数据集多场景（推荐），路径具体到数据集（ **../output/tum_rgbd_0/** ）；也可所有数据集场景一起评估，路径为 **../output/** 
- onekey.py->gt_dataset中，数据集路径（如 **tum_rgbd** ）不可带 **/** ，否则路径识别出成 **/** 下
```shell
python onekey.py -d ../datasets/ -r ../output/
```
- eval log
```shell
rendering rgbd_dataset_freiburg1_room:   0%|                                       | 0/1352 [00:00<?, ?it/s]Setting up [LPIPS] perceptual loss: trunk [alex], v[0.1], spatial [off]
/root/miniconda3/lib/python3.10/site-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
  warnings.warn(
/root/miniconda3/lib/python3.10/site-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=AlexNet_Weights.IMAGENET1K_V1`. You can also use `weights=AlexNet_Weights.DEFAULT` to get the most up-to-date weights.
  warnings.warn(msg)
Loading model from: /root/miniconda3/lib/python3.10/site-packages/lpips/weights/v0.1/alex.pth
rendering rgbd_dataset_freiburg1_room: 100%|████████████████████████████| 1352/1352 [01:26<00:00, 15.67it/s]
APE w.r.t. translation part (m)
(with SE(3) Umeyama alignment)

       max	0.134271
      mean	0.042810
    median	0.034197
       min	0.002788
      rmse	0.051668
       sse	3.609344
       std	0.028929
```
