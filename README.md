# Landmark Detection

### Adalberto Gonzalez

Computer Vision Nanodegree Program

# Overview
In this project, I've implemented SLAM (Simultaneous Localization and Mapping) for a 2 dimensional world!
I've combined robot sensor measurements and movement to create a map of an environment from only sensor and motion data gathered by a robot, over time. 
SLAM gives us a way to track the location of a robot in the world in real-time and identify the locations of landmarks such as buildings, trees, rocks, and other world features.
This is an active area of research in the fields of robotics and autonomous systems.

<img src="https://github.com/Adal-Glez/ComputerVision_ND_P3_Landmark_Detection/blob/master/3-4-graph-slam2x.jpg"/> 

# robot_class.py: Implementation of sense

Implemented the sense function to complete the robot class found in the robot_class.py file keeping the measurement_range only to 50.
I added the measurement_noise to both dx and dy parameters and handling prediction accuracy due negative values.

```python
 ## TODO: For each landmark
        for landmark_index in range(self.num_landmarks):
            ## 1. compute dx and dy, the distances between the robot and the landmark
            dx = self.landmarks[landmark_index][0] - self.x
            dy = self.landmarks[landmark_index][1] - self.y 

            ## 2. account for measurement noise by *adding* a noise component to dx and dy
            ##    - The noise component should be a random value between [-1.0, 1.0)*measurement_noise
            ##    - Feel free to use the function self.rand() to help calculate this noise component
            ##    - It may help to reference the `move` function for noise calculation
            dx = dx + self.rand() * self.measurement_noise
            dy = dy + self.rand() * self.measurement_noise
            ## 3. If either of the distances, dx or dy, fall outside of the internal var, measurement_range
            ##    then we cannot record them; if they do fall in the range, then add them to the measurements list
            ##    as list.append([index, dx, dy]), this format is important for data creation done later                
            
            #assert(abs(dx) <= self.measurement_range)
            if abs(dx) <= self.measurement_range and abs(dy) <= self.measurement_range:
                measurements.append([landmark_index,dx,dy])
            ## TODO: return the final, complete list of measurements
        return measurements
```

# Implementation of initialize_constraints
The array omega and vector xi are intialized such that any unknown values are 0 the size of these should vary with the given world_size, num_landmarks, and time step, N, parameters.

#Implementation of `slam
I've taken into account of motion_noise and measurement_noise to account for any sensory information if they are connected, like in the real world scenarios.
```python

```

The test results are close and make sense. 
The difference in the results is due to floating point or matrix inverse calculations. 
<img src="https://github.com/Adal-Glez/ComputerVision_ND_P3_Landmark_Detection/blob/master/robot-world.png"/> 

## Truth Values
<img src="https://github.com/Adal-Glez/ComputerVision_ND_P3_Landmark_Detection/blob/master/truth_values.png"/>

## Estimated poses
<img src="https://github.com/Adal-Glez/ComputerVision_ND_P3_Landmark_Detection/blob/master/estimated_poses.png"/> 

This was a good coding practice!
### Adalberto 

If you are interested in knowing more have a looka this link
[Concept of sensor fusion](https://blogs.nvidia.com/blog/2019/04/15/how-does-a-self-driving-car-see "Concept of sensor fusion")
