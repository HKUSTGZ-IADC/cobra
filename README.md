<div align="center">
  <!-- <a href="">
    <img align="left" src="docs/media/IADC_logo.png" height="100" alt="IADC">
  </a> -->
  <a href="">
    <img align="center" src="docs/media/cobra_logo.png" height="130" alt="cobra">
  </a> 
  <!-- <a href="">
    <img align="" src="docs/media/hkustgz_logo.png" height="80" alt="hkustgz">
  </a>   -->
  <!-- <a href="">
    <img align="right" src="docs/media/hkust_only_pattern.png" height="100" alt="hkustgz">
  </a>     -->
</div>

<!--
# Cobra

Cobra is a C++/Python library for metric-semantic-driven navigation in both unstructured and structured environments for mobile robots. Cobra is modular, ROS-enabled, and runs on CPU+GPU.

Cobra comprises four **modules**:
- A fast and accurate LiDAR-Vision-Inertial Odometry (LVIO) ([Cobra-State-Estimation](http://gitlab.ram-lab.com/ramlab_dataset_sensor/code/r3live))
- A semantic segmentation (perception) module (high-performance) ([Cobra-Semantics](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/hkustgz_segnet))
- A metric-semantic dense mapping system ([Cobra-Mapping](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/nvblox)) 
  and its ROS-enabled plugins ([Cobra-ROS-Mapping](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/glimpse_nvblox_ros1))
- A metric-semantic global planner ([Cobra-Planner](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/cobra_planner))
<!--
- A solver for trajectory optimization (local planner) and control ([TBC](xxx))
-->
<!-- - Tool functions:
  - A toolbox to support the debug and monitor of Cobra ([Cobra-Tool](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/cobra_tools)) -->
<!-- - A tool to convert LiDAR points into depth/height images ([Cobra-Tool-p2img](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/pointcloud_image_converter)) -->

<!-- Click on the following links to install Cobra's modules and get started!  -->

#### Results of Cobra

**Mapping**: Campus (without semantics)
```
roslaunch r3live r3live_bag_ouster128_raw.launch
roslaunch nvblox_ros nvblox_lidar_ros_fusionportable.launch
```
<div align="center">
    <a href="">
      <img src="docs/media/r3live_nvblox_Mapping.gif" width="50%" 
      alt="r3live_nvblox_Mapping">
   </a>
</div>

**Mapping**: SemanticKITTI Sequence07 (LiDAR-based semantics)
```
rosbag play semantickitti_sequence07.bag
roslaunch nvblox_ros nvblox_lidar_ros_kitti.launch
```
<div align="center">
    <a href="">
      <img src="docs/media/result_mesh_semantickitti07.gif" width="50%" 
      alt="result_mesh_semantickitti07">
   </a>   
</div>

**Mapping**: KITTI-360 (Image-based semantics) 
```
rosbag play nvblox_mesh_2013_05_28_drive_0003_sync.bag
roslaunch nvblox_ros nvblox_lidar_ros_kitti360.launch
```
<div align="center">
    <a href="">
      <img src="docs/media/result_mesh_2013_05_28_drive_0003_sync.gif" width="50%" 
      alt="result_mesh_2013_05_28_drive_0003_sync">
   </a>   
</div>

**Mapping**: FusionPortable (Image-based semantics)
<div align="center">
    <a href="">
      <img src="docs/media/result_semanticfusionportable_sequence01_4x_playrate.gif" width="47%" 
      alt="result_semanticfusionportable_sequence01_4x_playrate">
   </a>   
</div>
<p></p>
<div align="center">
    <a href="">
      <img src="docs/media/result_mesh_fusionportable.gif" width="50%" 
      alt="result_mesh_fusionportable">
   </a>   
</div>

**Navigation**: 
<div align="center">
    <a href="">
      <img src="docs/media/result_navigation_sequence01_test_1_5x.gif" width="47.5%" 
      alt="result_navigation_sequence01_test_1_5x">
   </a>   
</div>


## Chart

<!-- ![overall_chart]() -->

<!--
## 1. Installation
Clone the code
```shell script
git clone http://gitlab.ram-lab.com/ramlab_dataset_sensor/cobra --recursive 
wstool merge cobra/cobra_https.rosinstall
wstool update
cd cobra
```
Build the docker environment **(X86 PC)**: change the cuda version of **Dockerfile_x86** (first line) for you GPU 
```shell script
docker build -t cobra_x86:20240124-ros_noetic-py3-torch-cuda -f docker/Dockerfile_x86 .
```
Build the docker environment **(Jetson - ARM PC)**
```shell script
docker build -t cobra_jetson:20240124-ros_noetic-py3-torch-jetpackr35 -f docker/Dockerfile_jetson .
```
Create the docker container
```shell script
docker pull cobra_x86:20240124-ros_noetic-py3-torch-cuda
nvidia-docker run -e DISPLAY -v ~/.Xauthority:/root/.Xauthority:rw --network host \
  -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
  -v volume_path_to_host:volume_path_to_docker \
  --privileged --cap-add sys_ptrace \
  -it --name cobra cobra_x86:20240124-ros_noetic-py3-torch-cuda \
  /bin/bash
```
Compile the nvblox
```shell script
cd src/glimpse_nvblox_ros1/nvblox/nvblox
mkdir build && cd build && cmake .. && make -j3
```
Complie other packages
```shell script
catkin build r3live pointcloud_image_converter cobra_tools nvblox_ros -DCMAKE_BUILD_TYPE=Release
```
<!--
Please follow the below tutorial to install individual packages
* [Cobra-State-Estimation](http://gitlab.ram-lab.com/ramlab_dataset_sensor/code/r3live)
* [Cobra-Semantics](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/hkustgz_segnet)
* [Cobra-Mapping](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/nvblox)
* [Cobra-Planner](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/cobra_planner)
* [Cobra-Tool](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/cobra_tools)
* [Cobra-Tool-p2img](http://gitlab.ram-lab.com/ramlab_dataset_sensor/mapping_codebase/pointcloud_image_converter)
-->

## 2. Usage
Test with the **FusionPortable** Dataset
```shell script
bash scripts/run_cobra_fusionportable.sh
```
Test with the **SemanticFusionPortable** Dataset
```shell script
bash scripts/run_cobra_semanticfusionportable.sh
```
Test with the **SemanticKITTI** Dataset
```shell script
bash scripts/run_cobra_semantickitti.sh
```
Batch test with all datasets
```shell script
rosparam set use_sim_time true
cd src/cobra_tools/scripts/bash
bash run_nvblox_proposed.bash
```
Monitor the CPU, GPU, and memory of the PC
```shell script
rosrun cobra_tools monitor_pc_status.py -c /Spy/dataset/tmp/logs/cpu_gpu_utils_0.1
```

## 3. Key parameters
```
voxel_size: 0.3 (SemanticKITTI00, 02, 08), 0.25 (other sequences)
mesh: 0 (not save mesh result), 1 (save mesh result)
dataset_type: the id of different datasets
max_mesh_update_time: the frequency of saving mesh. For example: 0.1 for 10Hz
performance_monitor: 0 (not monitor CPU and GPU usage), 1 (monitor CPU and GPU usage)
```

## Citation

If you found any of the above modules useful, we would really appreciate if you could cite our work:

<!-- - [1] Jiao, J., Ruoyu, G., Yuanhang, L., Ren, X., Bowen, Y., ... & Liu, M. [**Real-Time Metric-Semantic Mapping for Autonomous Navigation in Outdoor Environments**](). submitted to TASE2024.

```bibtex
@inproceedings{jiao2022fusionportable,
  title={Real-Time Metric-Semantic Mapping for Autonomous Navigation in Outdoor Environments},
  author={Jiao, Jianhao and Wei, Hexiang and Hu, Tianshuai and Hu, Xiangcheng and Zhu, Yilong and He, Zhijian and Wu, Jin and Yu, Jingwen and Xie, Xupeng and Huang, Huaiyang and others},
  booktitle={2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  pages={3851--3856},
  year={2022},
  organization={IEEE}
}
``` -->

- [2] Jiao, J., Wei, H., Hu, T., Hu, X., Zhu, Y., ... & Liu, M. [**FusionPortable: A Multi-Sensor Campus-Scene Dataset for Evaluation of Localization and Mapping Accuracy on Diverse Platforms**](https://arxiv.org/abs/2208.11865). In 2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS). IEEE.

```bibtex
@inproceedings{jiao2022fusionportable,
  title={FusionPortable: A Multi-Sensor Campus-Scene Dataset for Evaluation of Localization and Mapping Accuracy on Diverse Platforms},
  author={Jiao, Jianhao and Wei, Hexiang and Hu, Tianshuai and Hu, Xiangcheng and Zhu, Yilong and He, Zhijian and Wu, Jin and Yu, Jingwen and Xie, Xupeng and Huang, Huaiyang and others},
  booktitle={2022 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  pages={3851--3856},
  year={2022},
  organization={IEEE}
}
```


## Open-Source Datasets

We release an open-source dataset: [FusionPortable](https://ram-lab.com/file/site/fusionportable/dataset/fusionportable) [1] for real-life tests. The dataset provides:
- 3D LiDAR
- Stereo Frame Cameras
- Stereo Event Cameras
- IMU data
- Ground-Truth Odometry
- Static TF (ground-truth poses of static objects)
<!-- - (Optional: Ground-truth 2D Semantic Segmentation))
- (Optional: TF (ground-truth odometry of robots, and agents)) -->

## Acknowledgments

## License

[BSD License](LICENSE.BSD)











