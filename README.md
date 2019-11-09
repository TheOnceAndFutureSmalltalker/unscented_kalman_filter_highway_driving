# Unscented Kalman Filter for Highway Driving

This project implements an Unscented Kalman Filter in C++ and runs it against a simulation of radar and lidar measurements taken from an ego car as it travels down the highway. The animation below shows the ego car in green and the surrounding traffic in blue.  


<p align="center">
<img src="https://github.com/TheOnceAndFutureSmalltalker/unscented_kalman_filter_highway_driving/blob/master/media/ukf-highway-tracked.gif"  /><br /><b>Cars Tracked by Unscented Kalman Filter</b></p>
<br />

## Dependencies and Requirements

This project was developed on Ubuntu 16.04.  It may work on Windows, Mac, and other Ubuntu versions but has not been tested as such.

The code requires the <a href="http://pointclouds.org/">Point Cloud Library or PCL</a>.  Installation instructions are included below.


## Installing PCL

To install the Point Cloud Library, follow the instructions below for your environment.  These instructions were copied from https://github.com/udacity/SFND_Lidar_Obstacle_Detection/edit/master/README.md.  You may also find additional installation instructions on the <a href="http://pointclouds.org/">Point Cloud Library or PCL</a> website.

### Ubuntu 
This installation for Ubuntu is quite lengthy - up to an hour - so be patient.  Several additional dependencies, like Eigen, are installed as well.

$> sudo apt install libpcl-dev


### Windows 

http://www.pointclouds.org/downloads/windows.html

### MAC

#### Install via Homebrew
1. install [homebrew](https://brew.sh/)
2. update homebrew 
	```bash
	$> brew update
	```
3. add  homebrew science [tap](https://docs.brew.sh/Taps) 
	```bash
	$> brew tap brewsci/science
	```
4. view pcl install options
	```bash
	$> brew options pcl
	```
5. install PCL 
	```bash
	$> brew install pcl
	```

#### Prebuilt Binaries via Universal Installer
http://www.pointclouds.org/downloads/macosx.html  
NOTE: very old version 

#### Build from Source

[PCL Source Github](https://github.com/PointCloudLibrary/pcl)

[PCL Mac Compilation Docs](http://www.pointclouds.org/documentation/tutorials/compiling_pcl_macosx.php)

## Compiling and Running The Project

To acquire, compile, and run the project in Ubuntu, follow the statements below.  Windows and Mac environments should be modified accordingly.

```bash
$> git clone https://github.com/TheOnceAndFutureSmalltalker/unscented_kalman_filter_highway_driving.git
$> cd lidar_obstacle_detection
$> mkdir build && cd build
$> cmake ..
$> make
$> ./environment 
```

If all goes well, you will see a window pop up with an animation of the modified point cloud that looks similar to the graphic at the top of this readme.

## Discussion

The Unscented Kalman Filter generates estimates of the other car's positions and velocities which are better than the measurements provided by either the radar or lidar.  Predictions of the other cars' motions are made using the CTRV, or constant turn rate and velocity, model. 

The Unscented Kalman Filter improves upon the Extended Kalman Filter in that the linear approximation provided by the EKF may not be adequate and calculating a Jocabian matrix is no longer required. Instead, the prediction is based on a sample of the current state. These sample points are called sigma points. The sigma points can then be tranformed into the measurement space and a new mean and covariance matrix calculated. From this the new prediction is made and then combined with the new measurements. The Unscented Kalman Filter also improves in overall error.
