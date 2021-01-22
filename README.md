# Landmark-Detection-Tracking-SLAM
This project implements SLAM (Simultaneous Localization and Mapping) for a 2 dimensional world which is used for robot sensor measurements and movement to create a map of an environment from only sensor and motion data gathered by a robot, over time. SLAM gives a way to track the location of a robot in the world in real-time and identify the locations of landmarks such as buildings, trees, rocks, and other world features. This is a basic concept implementation and this topic is an active area of research in the fields of robotics and autonomous systems.(refer to reference)

## Implementation Approach  
### Code Structure 
The project will be broken up into three Python notebooks; the first two are for exploration of provided code, and a review of SLAM architectures:
* Step 1 : [Robot Moving and Sensing](1.%20Robot%20Moving%20and%20Sensing.ipynb): Testing with imported code from `robot_class.py`
* Step 2 : [Omega and Xi, Constraints](2.%20Omega%20and%20Xi%2C%20Constraints.ipynb)
* Step 3 : [Landmark Detection and Tracking](3.%20Landmark%20Detection%20and%20Tracking.ipynb) with `robot_class.py`

### `robot_class.py`
####`sense` function 
* compute `dx` and `dy`, the distances between the robot and the landmark
    * The noise component should be a random value using `self.rand()` between (-1.0, 1.0)*`measurement_noise`
* account for measurement noise by *adding* a noise component to `dx` and `dy`
*  If either of the distances, dx or dy, fall outside of the internal var, `measurement_range`, don't add to list, otherwise, add them to the measurements list
* returns a measurement list of values that reflect the measured distance (dx, dy) between the robot's position and any landmarks it sees with a given amount of `measurement_noise` and the `measurement_range` of the robot. One format in the returned list looks like this: `[landmark_index, dx, dy]`.

### Landmark Detection and Tracking
#### `initialize_constraints`
Initialize the array `omega` and vector `xi` such that any unknown values are 0 the size of these should vary with the given `world_size`, `num_landmarks`, and time step, `N`, parameters.

#### SLAM(Simultaneous Localization and Mapping) 
* Iterate through the generated data and update the constraints in sensor measurement data.
    * The values in the constraint matrices is updated by sensor measurements from measurement_uncertainty
* Update the constraint matrices from robot motion data.
    * The values in the constraint matrices is updated by motion `(dx, dy)` and uncertainty in motion.
    * It shows the robot is moving as per the motion
* slam returns a list of robot and landmark positions, `mu`.
    * `mu` is the x, y positions of the robot over time and the estimated locations of landmarks in the world. 
    * `mu` is calculated with the constraint matrices `omega^(-1)*xi`
    
### Reference 
* [SLAM](http://rpg.ifi.uzh.ch/docs/TRO16_cadena.pdf)
* [Pose Estimation with Multiple Sensors](https://arxiv.org/pdf/1901.03642.pdf)
* [General SLAM Framework](https://arxiv.org/abs/1902.07995)
* [robotic SLAM](https://jneuroengrehab.biomedcentral.com/articles/10.1186/1743-0003-7-10)

