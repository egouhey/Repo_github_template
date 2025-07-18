# Guide for setting up and using go2 in simulation and using slam

## Installation

In order to have a gazebo11 simulation with a Go1 or B2 Unitree robot in a ROS2 Humble environment, please clone this repository :

```bash
git clone https://github.com/Atharva-05/unitree_ros2_sim.git
```

In addition, add the [B2 package provided in this repository](https://github.com/egouhey/Navigation_Suez_Robotics/blob/main/src/B2-Gazebo/b2_sim.zip).

Then follow the steps they provided.

Please use Colcon to build all packages.
We recommend using the command:
```bash
colcon build --symlink-install --merge-install
```

To use slam with Go1, please add in [data_files](https://github.com/Atharva-05/unitree_ros2_sim/blob/main/go1_sim/go1_navigation/setup.py#L9) :
```python
('share/' + package_name, ['launch/navigation_new.launch.py']),
```

For usinge Go1 navigation, in the [navigation2 parameter file](https://github.com/Atharva-05/unitree_ros2_sim/blob/main/go1_sim/go1_navigation/params/nav2_params.yaml) please add this configuration :

```yaml
slam_toolbox:
  ros__parameters:
    base_frame: base_link
```


## How to use

To run the simulation of Go1, please follow the steps indicated in the [ReadMe](https://github.com/Atharva-05/unitree_ros2_sim/blob/main/README.md) of the repository.
To run the simulation of B2, please run:
```bash
ros2 launch b2_gazebo spawn_b2.launch.py
```

To use slam and run the parameters edited in the previous section please launch in a 3rd terminal:
For Go1:
```bash
ros2 launch go1_navigation navigation_new.launch.py slam:="True"
```
or for B2
```bash
ros2 launch b2_navigation navigation_new.launch.py slam:="True"
```
The display of Go1 should look like this in gazebo:
<div style="text-align: center;">
  <img src="/images/gazebo_go1.png" alt="Simulation Go1 Gazebo" width="300"/>
</div>

And it should render like this in rviz by adding a map object based on topic /map :
<div style="text-align: center;">
  <img src="/images/rviz_slam_go1.png" alt="Affichage rviz Go1" width="300"/>
</div>

The display of B2 should look like this:
<div style="text-align: center;">
  <img src="/images/gazebo_b2.png" alt="Simulation B2 Gazebo" width="300"/>
</div>
In rviz it should render like this:
<div style="text-align: center;">
  <img src="/images/rviz_b21.png" alt="Simulation B2 RVIZ" width="300"/>
</div>

It is then possible to set Goal Poses on the rviz interface and watch the robot Go1 reaching them.
The map used by slam is changing and adapting to what lidar data the robot get.

## Save the map

To save the map, please run this command :
```bash
ros2 run nav2_map_server map_saver_cli -f name_of_the_map
```