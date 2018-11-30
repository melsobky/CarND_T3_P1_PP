# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program

## Overview

This project simulates a highway with numerous cars running at speeds +- 10 mph of a 50 mph speed limit. 

The goal is to program car to:

* Stay as close to the speed limit without exceeding it
* Drive inside the lane lines, except when changing lanes
* Avoid all collisions, including going too slow and being rear-ended
* Accelerate and decelerate smoothly within defined acceleration and jerk limits
* Change lanes safely when the leading car is moving slowly

## Rubic points
### The code compiles correctly.
Code compiles without errors with cmake and make. No changes were made to CMakeLists.txt.

### The car is able to drive at least 4.32 miles without incident
The image below shows the car at 5.15 miles without a single incident.
![5.15 miles](images/miles.png)
### The car drives according to the speed limit
The car never exceeds the 50 mph speed limit. The speed drops when obstructed by traffic ahead, with no free lanes available to shift to.
### Max Acceleration and Jerk are not Exceeded
The car does not exceed a total acceleration of 10 m/s^2 and a jerk of 10 m/s^3.
### Car does not have collisions
The car did not come into contact with any of the other cars on the road.
### The car stays in its lane, except for the time between changing lanes
The car leaves the lanes ONLY during changing lanes.

### The car is able to change lanes
The car is able to smoothly change lanes when it makes sense to do so, such as when behind a slower moving car and an adjacent lane is clear of other traffic.


## Reflection

### Prediction [lines 178-214](./src/main.cpp#L178) & [lines 306-223](./src/main.cpp#L306)
Through using the car's state and sensor fusion data, possible collisions are predicted, and respective flags are raised. Frenet coordinates of the surrounding vehicles are used to determine their respective lanes and distance from the car. 

The outputs of this is a flag to determine if it's safe to shift to a certain lane or not.

### Behavior Planning [lines 326-353](./scr/main.cpp#L326)
Based on the previous predictions, corrective behaviour is needed. 

If It's not safe to shift lanes the car will slow down until it's safe again. When It's safe to change lanes the vehicle will execute the shift task.

### Trajectory Generation [line 367 to line 478](./scr/main.cpp#L367)
The first two points in the path are the last two points in the previous path.
Given the target lane, three evenly spaced points (30 meters apart) are added to the path.
A spline is used smooth out the lines between the three points using the spline.h library.
Waypoints are extracted as the first 30 meters of the spline and are sent to the simulator.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

Here is the data provided from the Simulator to the C++ Program

## Simulator.
You can download the Term3 Simulator which contains the Path Planning Project from the [releases tab (https://github.com/udacity/self-driving-car-sim/releases/tag/T3_v1.2).

---
