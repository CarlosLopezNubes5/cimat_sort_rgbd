# cimat_sort_rgbd
![size](https://img.shields.io/github/license/JCLArriaga5/cimat_sort_rgbd) ![size](https://img.shields.io/github/repo-size/JCLArriaga5/cimat_sort_rgbd)

A [ROS](http://wiki.ros.org/) package for tracking people in RGB-D images with [SORT](https://github.com/abewley/sort) (Simple Online and Realtime Tracking) algorithm.

To obtain a bachelor's degree through a stay at CIMAT, this project was carried out. Under the supervision of a CIMAT researcher.

Developing improvements for the project ...

## Dependencies
* [Ubuntu](https://ubuntu.com/) 16.04 LTS.
* [PCL](https://github.com/PointCloudLibrary/pcl) 1.7.2.
* [OpenCV](https://github.com/opencv/opencv) 3.3.1.

## Instalation
```sh
$ cd ~/catkin_ws/src
$ git clone https://github.com/JCLArriaga5/cimat_sort_rgbd.git
$ cd ..
$ catkin_make
```

## pcl_people_detection
The program pcl_people_detector is the code created by [PCL](https://pcl-tutorials.readthedocs.io/en/latest/ground_based_rgbd_people_detection.html#ground-based-rgbd-people-detection) to detect people on a ground plane with RGB-D data, to test it requires having connected an rgbd sensor (e.g. Kinect, Realsense).

Execute following command:
```sh
$ rosrun cimat_sort_rgbd pcl_people_detection
```

## simulate_pcl_people_detection.
To simulate the plc detector, using an RGB-D image dataset it is necessary to download the dataset previously. For the simulation with a dataset, we make use of the EPFL-LAB dataset, [here](../master/utils/dataset/README.md) you can see where to download it.

Once the dataset is downloaded in the corresponding folder, you can execute the following command to run the simulation with the dataset
```sh
$ rosrun cimat_sort_rgbd dataset_pcl_people_detection
```

## Sort test on RGB-D images with PCL detector.

The state vector of each objective for the Kalman filter that was used was the following:

<p align="center"><img src="images\state_vector_rgbd.png" width="300" height="30"></p>

where <img src="https://render.githubusercontent.com/render/math?math=(u, v, w)"> are the coordinates of the centroid of the enclosing box or cylinder, taken from the top or bottom. The height <img src="https://render.githubusercontent.com/render/math?math=h"> the <img src="https://render.githubusercontent.com/render/math?math=$\gamma$"> radius were taken as constants, so <img src="https://render.githubusercontent.com/render/math?math=$(\dot{u}, \dot{v}, \dot{w})$"> are the respective velocities of the centroid. For the data association, an IoU of the upper circles of the cylinder of each objective was used.

<p align="center"><img src="images/3d-sort.png" height="250"></p>

To [test](../master/src/sort/sort_proofs.cpp) the SORT algorithm with EPFL-LAB dataset and PLC detector use the following command.
```sh
$ rosrun cimat_sort_rgbd dataset_sort_test
```
