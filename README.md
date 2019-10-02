# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Introduction

In this project, I designed a PID controller to control the simulator vihicle, both longitudinally and laterally. Longitudinally, I used the PID controller to control the vehicle's throttle to follow a reference speed. Laterally, the PID controller outputs steering angle based on the CTE and tries to bring the CTE to 0.

Both controllers share the same set of hyperparameters. The car is able to finish multiple laps without hitting the curb.

## Key rubic points check

### 1. Code must compile --- YES

Please Fork/Download my branch and follow the "basic build instructions" in the Appendix to build and run the project.

### 2. The PID procedure follows what was taught in the lessons --- YES

The PID controller I designed contains 3 main steps: Initialize, Update individual error, and Update final error.

### 3. Describe the effect each of the P, I, D components had in your implementation --- See below

P - proportional. This component acts directly on the actual error and tries to reduce the error. But it'll bring overshoot and oscillation.

I - integral. This component acts on the integration of actual error and is able to reduce system bias, the integration of which tends to increase over time.

D - derivative. This component acts on the changing rate of the actual error, to reduce overshoot and oscillation.

### 4. Describe how the final hyperparameters were chosen --- See below

As the first step, I initialized the PID as P only controller, which means only P component is non-zero. First I gave it a value of 1, just to try out. And it turned out that the car overshoots quickly and oscillates badly.

Then I reduced the P value to 0.1, which seemed to work fine on straight lanes. However, whenever there's a curve, the car starts oscillate. So I decided to bring in the D component to reduce overshoot and oscillation. Multiple values are tested, and it appears that neither too big nor too small D values are able to reduce oscillation well. Finally I chose 0.8 as D value, which combines with P value can drive the car in a pretty stable way in most parts of the track.

However, with P and D decided, the car will still tend to go off the track in some sharp turns. This reminds me of bringing in the I term, which in my mind could help in these cases. Because in sharp turns there will be an accumulation of CTE, which can be tackled by the I term. Eventually I set the I term as 0.0023 through tuning.

So the final decision on the hyperparameters is:

P: 0.1
I: 0.0023
D: 0.8

### 5. The vehicle must successfully drive a lap around the track --- YES. Actually multiple laps.


# Appendix

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)


## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.