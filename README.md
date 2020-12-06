
# CarND-PID-Control
Udacity Self-Driving Car Nanodegree - PID Control project

# Overview

This project implements a [PID controller](https://en.wikipedia.org/wiki/PID_controller) to control a car in Udacity's simulator([Download here](https://github.com/udacity/self-driving-car-sim/releases)). The simulator sends cross-track error, speed and angle to the PID controller(PID) using [WebSocket](https://en.wikipedia.org/wiki/WebSocket) and it receives the steering angle ([-1, 1] normalized) and the throttle to drive the car. The PID uses the [uWebSockets](https://github.com/uNetworking/uWebSockets) WebSocket implementation. Udacity provides a seed project to start from on this project ([here](https://github.com/udacity/CarND-PID-Control-Project)).

# Prerequisites

The project has the following dependencies (from Udacity's seed project):

- cmake >= 3.5
- make >= 4.1
- gcc/g++ >= 5.4
- Udacity's simulator.

For instructions on how to install these components on different operating systems, please, visit [Udacity's seed project](https://github.com/udacity/CarND-PID-Control-Project). 

# Compiling and executing the project

Since I am using the workspace provided by the Udacity in course I am using the same build instructions from project github page.

## Compilation

### Your code should compile.

The code compiles without errors or warnings. No modifications were done on the provided setup.

## Implementation

### The PID procedure follows what was taught in the lessons.

The PID implementation is done on the [./src/PID.cpp](./src/PID.cpp). The [PID::UpdateError](./src/PID.cpp#L24) method calculates proportional, integral and derivative errors and the [PID::TotalError](./src/PID.cpp#L33) calculates the total error using the appropriate coefficients.

## Reflection

### Describe the effect each of the P, I, D components had in your implementation.

- The proportional portion of the controller tries to steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly. An example image where this component is used along is [P-overshoot car from track](images/p_overshoot.png).

- The integral portion tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present. An example video where this component is used along is [I-overshoot car from track](images/i_overshoot.png).

- The differential portion helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it. An example video where this component is used along is [D-overshoot car from track](images/d_overshoot.png).

### Describe how the final hyperparameters were chosen.

The parameters were chosen manually by try and error. First, make sure the car can drive straight with zero as parameters. Then add the proportional and the car start going on following the road but it starts overshooting go out of it. Then add the differential to try to overcome the overshooting. The integral part only moved the car out of the road; so, it stayed close to zero. After the car drove the track without going out of it, the parameters increased to minimize the average cross-track error on a single track lap. The final parameters where [P: 0.15, I: 0.0001, D: 3].

## Simulation

### The vehicle must successfully drive a lap around the track.

Vehicle did finish two laps around the track successfully.
