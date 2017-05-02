# **Pedestrian Tracking with Kalman Filter**

Utilize fused data from both LIDAR and RADAR sensors for pedestrian tracking based on the Extended Kalman Filter framework.

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


