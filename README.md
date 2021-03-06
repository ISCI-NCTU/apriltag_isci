# AprilTag for ISCI Camera
## Maintainer
- [Howard Chen](https://github.com/s880367) < s880367@gmail.com >
, [Intelligent Control System Integration Lab](http://isci.cn.nctu.edu.tw/), NCTU.
- This package contains the apriltag detection package under ROS indigo for camera in ISCI lab.
- Originally forked from [VTAstrobotics/apriltags_ros](https://github.com/VTAstrobotics/apriltags_ros)

## Installation
```
cd ~/your-ros-workspace/src
git clone https://github.com/ISCI-NCTU/apriltag_isci.git
catkin_make
```
## Description

### Highlights
- Support kinectV2, USB-cam and basler pylon camera
- For ROS kinetic package, Please check [ISCI-NCTU/apriltags_ros-1](https://github.com/ISCI-NCTU/apriltags_ros-1)
- Support multiple camera detection on same tag.

### Parameter
- ```<arg name="camera_name"``` : camera node name
- ```<arg name="image_view" default="true" />```: pop up the ```tag_detection_image``` whenever you launch
- ```<arg name="inverse_tf" default="false" />```: inverse the tf broadcast if set to true.

### Dependencies
- ROS indigo

## Usage

### 1. Usb camera
- You could run ```usbcam_test.launch``` for testing your usb-cam is connect or not.
- For running the apriltag detection:
```
roslaunch apriltags_ros usb_camera.launch
```


### 2. KinectV2
- You need to install the kinectV2 driver : [OpenKinect/libfreenect2](https://github.com/OpenKinect/libfreenect2)
- And the ROS bridge package [ISCI-NCTU/isci_kinect2](https://github.com/ISCI-NCTU/isci_kinect2)
- Launch the kinectV2 first :
```
roslaunch kinect2_bridge kinect_bridge.launch publish_tf:=true
```
- Then run the apriltag_detector:
```
roslaunch apriltags_ros kinectV2.launch
```

### 3. Basler Pylon camera (TM5 camera)
- You need to install the basler pylon camera driver and ROS package: [ISCI-NCTU/TM5_PylonCamera](https://github.com/ISCI-NCTU/TM5_PylonCamera)
- You can ```git clone``` the pylon camera package: ```TM5_PylonCamera``` under the same directory: ```workspace/src``` of this package, so that you don't have to ```source ``` the dependancy again.
- Then launch the apriltag detector:
```
roslaunch apriltags_ros pylon_camera.launch
```
- Be noticed of the camera topic name you publish and the name your apriltag detector node subscribe. They should be the same topic name so taht apriltag detector could receieve the image topic which the camera published.

### 4. Multiple camera
- Set the parameter ```inverse_tf``` true when ```roslaunch ``` to make all the camera become child frame and tag become common parent frame.

```
roslaunch apriltags_ros usb_camera.launch inverse_tf:=true
roslaunch apriltags_ros kinectV2.launch inverse_tf:=true
roslaunch apriltags_ros pylon_camera.launch inverse_tf:=true
```
