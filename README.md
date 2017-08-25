# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
   
### Simulator.
You can download the Term3 Simulator which contains the Path Planning Project from the [releases tab (https://github.com/udacity/self-driving-car-sim/releases).

### Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 50 m/s^3.

### Path Generation Logic
With every loop of the path planner, I first look at all the cars around me to determine if I am approaching a slow moving car in my current lane. If my vehicle is approaching a slow moving vehicle, I reexamine all the vehicles around me to determine the best course of action. I look at all the cars around me and determine if there's enough space to the left or right to switch lanes. If there's enough space in either the left or right lane, I record which lane I should move into (if both lanes are possible, I choose the left). If there's too many cars around me, I decrease my speed.  


Next, I generate a trajectory to feed to the vehicle's control system. I take all remaining points from the previous path, adding new points to the path based on the lane and speed decisions from the path planner. Utilizing the remaining points and only adding a couple new points keeps the car driving smoothly. I take this list of points and use a spline to generate a smooth trajectory, minimizing the car's acceleration and jerk. This trajectory is fed to the vehicle's controls.
