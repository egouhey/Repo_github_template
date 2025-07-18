# Documentation of go1 and b2 simulation with gazebo 

Go1 simulation is working properly in gazebo in a repository found : https://github.com/Atharva-05/unitree_ros2_sim/tree/main

B2 simulation is a work on progress.

The following sections will explain and detail the work.

## Go1 simulation

Based on the [unitree_ros2_sim repository](https://github.com/Atharva-05/unitree_ros2_sim/tree/main), please follow the user guide for details about how to build and launch it.

A different world can be added in the [world directory](https://github.com/Atharva-05/unitree_ros2_sim/tree/main/go1_sim/go1_gazebo/worlds), in sdf format.

The major part of the parameters used for navigation are set in a [parameter file](https://github.com/Atharva-05/unitree_ros2_sim/blob/main/go1_sim/go1_navigation/params/nav2_params.yaml).

The navigation part is working properly but could be tuned to fit better the robot or the map.

The slam part is not fully implemented and parameters should also be tuned.
The slam ros2 node should be used without a map to fit the requirements of the project. For now, it is not the case, working without a map is raising errors.
When working with a different world, the dependance to this map is problematic because it generating conflicts and errors when trying to navigate or use slam.


## B2 simulation

A first attempt on adapting the [unitree ros respository description ](https://github.com/unitreerobotics/unitree_ros/tree/master/robots/b2_description) of the b2 robot in a ros2 simulation has been made. But adapting the controllers and topics requires too much time and the documentation is too poor.
An second attempt to create a package with b2 simulation based on the go1 has been made and is shared in this repository in the [B2-Gazebo folder](https://github.com/egouhey/Navigation_Suez_Robotics/tree/main/src/B2-Gazebo).
The description of the b2 robot is adapted from the [unitree ros1 repository](https://github.com/unitreerobotics/unitree_ros/tree/master/robots/b2_description).

Furthermore the overall logic in the package [unitree_guide](https://github.com/Atharva-05/unitree_ros2_sim/tree/main/unitree_guide2) need to be adapted to the b2 with the specifications of the B2 robot (height, mass, offsets,etc.). When trying the parameters of the Go1 the robot is not standing fully (in "FIXEDSTAND" mode), it is sitting. Further modifications to the entry parameters must be made to have a full stand and have a moving robot.

Lidar and slam are as presented for the Go1 robot.