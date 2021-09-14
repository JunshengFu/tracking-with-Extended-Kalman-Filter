# **Object Tracking with Extended Kalman Filter**

### Objective
Utilize sensor data from both LIDAR and RADAR measurements for object (e.g. pedestrian, vehicles, or other moving objects) 
tracking with the Extended Kalman Filter.

### **Demo: Object tracking with both LIDAR and RADAR measurements**

[![gif_demo1][both_gif]](https://www.youtube.com/watch?v=XswKMtQBTCo)

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

(Note: the hyperlinks **only** works if you are on the homepage of this GitHub reop,
and if you are viewing it in "github.io" you can be redirected by clicking the **View the Project on GitHub** on the top)

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


### 5. Release History

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

---

## System details

### 1. Demos

### **Demo 1: Tracking with both LIDAR and RADAR measurements**
In this demo, both LIDAR and RADAR measurements are used for object tracking.

[![gif_demo1][both_gif]](https://www.youtube.com/watch?v=XswKMtQBTCo)

 

### **Demo 2: Tracking with only LIDAR measurements**

In this demo, only LIDAR measurements are used for the object tracking. 
 
![gif_demo2][lidar_gif]



### **Demo 3：Tracking with only RADAR measurements**

In this demo, only RADAR measurements are used for the object tracking.
are more noisy than the LIDAR measurements.

![gif_demo3][radar_gif]



#### From these three Demos, we could see that 

* RADAR measurements are tend to be more more noisy than the LIDAR measurements.
* Extended Kalman Filter tracking by utilizing both measurements from both LIDAR and RADAR can reduce the noise/errors 
from the sensor measurements, and provide the robust estimations of the tracked object locations.   

**_Note_**: the advantage of RADAR is that it can estimate the object speed directly by 
[Doppler effect](https://en.wikipedia.org/wiki/Doppler_effect).


### 2. How does LIDAR measurement look like

![][image4]

The LIDAR will produce 3D measurement px,py,pz. But for the case of driving on the road, we could simplify the pose of 
the tracked object as: px,py,and one rotation. In other words, we could only use px and px to indicate the position of 
the object, and one rotation to indicate the orientation of the object. But in real world where you have very steep road, 
you have to consider z axis as well. Also in application like airplane and drone, you definitely want to consider pz as well.



### 3. How does RADAR measurement look like

![][image5]

### 4. Comparison of LIDAR, RADAR and Camera

|            Sensor type           |  LIDAR |    RADAR  |   Camera   |
|:--------------------------------:|:------:|:---------:|:----------:|
|            Resolution            | median |  low      |  **high**  |
|      Direct velocity measure     |   no   |  **yes**  |     no     |
|            All-weather           |   bad  |  **good** |     bad    |
|            Sensor size           |  large | **small** |  **small** |
| sense non-line of  sight object  |   no   |  **yes**  |     no     |


**_Note_**:

* LIDAR wavelength in infrared; RADAR wavelength in mm. 
* LIDAR most affected by dirt and small debris.


One comparison Figure from _**another aspect**_.

![][image6]


### 5. How does the Extended Kalman Filter Work


![][image2]


### 4. Extended Kalman Filter V.S. Kalman Filter


![][image3]


* _x_ is the mean state vector.
* _F_ is the state transition function.
* _P_ is the state covariance matrix, indicating the uncertainty of the object's state.
* _u_ is the process noise, which is a Gaussian with zero mean and covariance as Q.
* _Q_ is the covariance matrix of the process noise.

**For EKF**
* To calculate predicted state vector _x′_, the prediction function _f(x)_, is used instead of the _F_ matrix.
* The _F_ matrix will be replaced by _Fj_ (jocobian matrix of _f_) when calculating _P′_.

---------------------------------------------------------

* _y_ is the innovation term, i.e. the difference between the measurement and the prediction. In order to compute the innovation term, we transform the state to measurement space by measurement function, so that we can compare the measurement and prediction directly.
* _S_ is the predicted measurement covariance matrix, or named innovation covariance matrix.
* _H_ is the measurement function.
* _z_ is the measurement.
* _R_ is the covariance matrix of the measurement noise.
* _I_ is the identity matrix.
* _K_ is the Kalman filter gain.
* _Hj_ and _Fj_ are the jacobian matrix.

**For EKF**
* To calculate innovation _y_, the measurement function _h(x')_ is used instead of the _H_ matrix.
* The _H_ matrix in the Kalman filter will be replaced by the _Hj_(Jacobian matrix of _h(x')_)when calculating _S_, _K_, and _P_.


**All Kalman filters have the same three steps:**

1. Initialization
2. Prediction
3. Update

A **standard Kalman filter** can only handle linear equations. Both the **Extended Kalman Filter** (EKF) and the **Unscented Kalman Filter** (UKF will be disuccsed in the next project) allow you to use non-linear equations; the difference between EKF and UKF is how they handle non-linear equations: Extended Kalman Filter uses the Jacobian matrix to linearize non-linear functions; Unscented Kalman Filter, on the other hand, does not need to linearize non-linear functions, insteadly, the unscented Kalman filter takes representative points from a Gaussian distribution. 




[//]: # (Image References)
[image1]: ./data/ekf_combine.png
[image2]: ./data/ekf_flow.jpg
[image3]: ./data/ekf_vs_kf.jpg
[image4]: ./data/lidar.jpg
[image5]: ./data/radar.jpg
[image6]: ./data/camera-vs-radar-vs-lidar_1.png
[radar_gif]: ./data/radar.gif
[lidar_gif]: ./data/lidar.gif
[both_gif]: ./data/both_lidar_radar.gif
