# **Object Tracking with Sensor Fusion-based Extended Kalman Filter**

### Objective
Utilize sensor data from both LIDAR and RADAR measurements for object (e.g. pedestrian, vehicles, or other moving objects) 
tracking with the Extended Kalman Filter.

### **Demo 1: Tracking with both LIDAR and RADAR measurements**
In this demo, the blue car is the object to be tracked, but the tracked object can be any types, e.g. 
pedestrian, vehicles, or other moving objects. We continuously got both LIDAR (**red circle**) and RADAR (**blue circle**) 
measurements of the car's location in the defined coordinate, but there might be noise and errors 
in the data. Also, we need to find a way to fuse the two types of sensor measurements to estimate 
the proper location of the tracked object.

Therefore, we use Extended Kalman Filter to compute the estimated location (**green triangle**) of the blue car. 
The estimated trajectory (**green triangle**) is compared with the ground true trajectory of the blue car, and 
the error is displayed in RMSE format in real time.

In autonomous driving case, the self-driving cars obtian both Lidar and radar sensors measurements of objects
to be tracked, and then apply the Extended Kalman Filter to track the objects based on the two types
 of sensor data.

[![gif_demo1][both_gif]](https://www.youtube.com/watch?v=XswKMtQBTCo)

 

### **Demo 2: Tracking with only LIDAR measurements**

In this demo, only LIDAR measurements are used for the object tracking.  
[![gif_demo2][lidar_gif]]



### **Demo 3：Tracking with only RADAR measurements**

In this demo, only RADAR measurements are used for the object tracking.
are more noisy than the LIDAR measurements.
[![gif_demo3][radar_gif]]




#### From these three Demos, we could see that 
* RADAR measurements are tend to be more more noisy than the LIDAR measurements.
* Extended Kalman Filter tracking by utilizing both measurements from both LIDAR and RADAR can reduce the noise/errors 
from the sensor measurements, and provide the robust estimations of the tracked object locations.   

**_Note_**: the advantage of RADAR is that it can estimate the object speed directly by 
[Doppler effect](https://en.wikipedia.org/wiki/Doppler_effect).

---


## Code & Files
### 1. Dependencies & environment

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [Eigen library](src/Eigen)


### 2. My project files

* [CMakeLists.txt](CMakeLists.txt) is the cmake file.

* [data](data) folder contains test lidar and radar measurements.

* [Docs](Docs) folder contains docments which describe the data.

* [src](src) folder contains the source code.


### 3. Code Style

* [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).


### 4. How to run the code

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make` 
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it by either of the following commands: 
   * `./ExtendedKF  ../data/obj_pose-laser-radar-synthetic-input.txt ./output.txt`
   * `./ExtendedKF  ../data/sample-laser-radar-measurement-data-1.txt ./output.txt`

---

## Release History

* 0.2.1
    * Docs: Add a sample video for vehicle tracking
    * Date 3 May 2017

* 0.2.0
    * Fix: Normalize the angle for EKF updates with Radar
    * Fix: Initialize several variables
    * Date 2 May 2017

* 0.1.1
    * First proper release
    * Date 1 May 2017

* 0.1.0
    * Initiate the repo and add the functionality of pedestrian trakcing with lidar data.
    * Date 28 April 2017



[//]: # (Image References)
[image1]: ./examples/car_not_car.png
[radar_gif]: ./data/radar.gif
[lidar_gif]: ./data/radar.gif
[both_gif]: ./data/both_lidar_radar.gif