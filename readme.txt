# 🤖 Autonomous Mapping and Navigation Workspace

A ROS 2 workspace for autonomous robot mapping, localization, and navigation in simulated environments using Gazebo Sim, SLAM Toolbox, and Nav2.

The project integrates custom navigation utilities, waypoint automation, localization tools, trajectory tracking services, and interactive teleoperation interfaces to provide a complete autonomous navigation pipeline.

---

## 🚀 Features

- 🗺️ Autonomous SLAM Mapping
  - Environment mapping using SLAM Toolbox
  - Occupancy grid generation and map saving

- 📍 Localization
  - AMCL-based localization
  - EKF sensor fusion support

- 🧭 Autonomous Navigation
  - Nav2-based global and local planning
  - Dynamic obstacle avoidance
  - Goal-based navigation

- 📌 Waypoint Missions
  - Multi-goal autonomous patrol routes
  - Configurable waypoint sequences

- 🎮 Interactive Teleoperation
  - RViz interactive marker controls
  - Manual robot override capability

- 📈 Trajectory Tracking
  - Path history generation
  - Odometry monitoring and visualization

- 🏠 Simulation Environment
  - Custom residential-style Gazebo world
  - Integrated robot model and sensor stack

---

## 🏗️ Project Architecture

The workspace is divided into multiple ROS 2 packages.

### bme_ros2_navigation

Core navigation package containing:

- Robot description files (URDF/Xacro)
- Gazebo simulation worlds
- RViz configurations
- Navigation parameters
- Localization parameters
- SLAM configurations

Key files:

text config/ ├── navigation.yaml ├── amcl_localization.yaml ├── ekf.yaml ├── slam_toolbox_mapping.yaml └── waypoints.yaml  worlds/ └── home.sdf  rviz/ └── rviz.rviz 

---

### bme_ros2_navigation_py

Python automation package containing:

- Automated waypoint execution
- Initial pose publication
- Mission orchestration utilities

Nodes:

text follow_waypoints.py publish_initial_pose.py 

---

### mogi_trajectory_server

Trajectory management package responsible for:

- Recording robot motion
- Maintaining path history
- Publishing trajectory information

Node:

text trajectory.py 

---

### interactive_marker_twist_server

Provides RViz-based manual control interfaces through interactive markers.

Features:

- Interactive movement commands
- Teleoperation override
- Real-time velocity control

---

## 📂 Workspace Structure

text autonomous-mapping-and-navigation/ │ ├── src/ │ ├── bme_ros2_navigation/ │   ├── config/ │   ├── launch/ │   ├── rviz/ │   ├── urdf/ │   └── worlds/ │ ├── bme_ros2_navigation_py/ │ ├── mogi_trajectory_server/ │ └── interactive_marker_twist_server/ 

---

## ⚙️ Prerequisites

### Operating System

- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS

### ROS Distribution

- ROS 2 Jazzy Jalisco
- ROS 2 Iron Irwini

### Simulator

- Gazebo Sim Harmonic
- Gazebo Sim Garden

### Required Tools

- colcon
- rosdep
- RViz2
- Nav2
- SLAM Toolbox

---

## 📦 Installation

### Clone Repository

bash mkdir -p ~/target_ws/src cd ~/target_ws/src  git clone <repository-url> 

---

### Install Dependencies

bash cd ~/target_ws  rosdep install \   --from-paths src \   --ignore-src \   -r -y 

---

### Configure Gazebo Resource Paths

bash echo "export GZ_SIM_RESOURCE_PATH=\$HOME/target_ws/install/bme_ros2_navigation/share:\$GZ_SIM_RESOURCE_PATH" >> ~/.bashrc  source ~/.bashrc 

---

### Build Workspace

bash cd ~/target_ws  colcon build --symlink-install  source install/setup.bash 

---

## 🚀 Running the Project

Before launching any node:

bash source ~/target_ws/install/setup.bash 

---

## Stage 1 — Mapping

Launch the robot in the simulation environment and begin SLAM mapping:

bash ros2 launch bme_ros2_navigation mapping.launch.py 

Use:

- RViz interactive markers
- Keyboard teleoperation
- Joystick controls

to explore the environment and generate a complete occupancy map.

---

## Stage 2 — Autonomous Navigation

After saving the generated map:

bash ros2 launch bme_ros2_navigation navigation.launch.py 

This launches:

- AMCL Localization
- Nav2 Planner
- Controller Server
- Behavior Tree Navigator
- Costmaps

---

## 🤖 Automated Waypoint Missions

Execute preconfigured waypoint sequences:

bash ros2 run bme_ros2_navigation_py follow_waypoints 

Waypoints are loaded from:

text config/waypoints.yaml 

---

## 📍 Publish Initial Pose

To initialize robot localization:

bash ros2 run bme_ros2_navigation_py publish_initial_pose 

This publishes the robot's initial pose estimate to AMCL.

---

## ⚙️ Configuration

### Navigation Parameters

Modify:

text config/navigation.yaml 

Examples:

- Maximum velocity
- Acceleration limits
- Goal tolerances
- Obstacle inflation radius
- Planner behavior

---

### Localization Parameters

Modify:

text config/amcl_localization.yaml 

Examples:

- Particle count
- Sensor noise
- Update thresholds

---

### EKF Fusion Parameters

Modify:

text config/ekf.yaml 

For:

- IMU integration
- Odometry fusion
- State estimation tuning

---

### Waypoint Missions

Modify:

text config/waypoints.yaml 

to define custom patrol routes.

---

## 🔄 Navigation Pipeline

mermaid flowchart LR  A[Gazebo Simulation] --> B[Robot Sensors]  B --> C[SLAM Toolbox] B --> D[EKF]  C --> E[Map] D --> F[Localization]  E --> G[Nav2] F --> G  G --> H[Path Planner] H --> I[Controller Server]  I --> J[Robot Motion]  J --> K[Trajectory Server] 

---

## 📊 Applications

This workspace can be used for:

- Autonomous indoor navigation
- Service robot research
- Multi-goal waypoint missions
- SLAM experimentation
- Localization benchmarking
- ROS 2 navigation studies
- Academic robotics projects

---

## 🔮 Future Improvements

Potential future enhancements:

- Dynamic obstacle prediction
- Multi-robot coordination
- Frontier-based exploration
- Vision-based localization
- Semantic mapping
- Outdoor GPS integration
- Reinforcement learning navigation

---

## 👨‍💻 Authors

Developed as part of an autonomous robotics and navigation project using ROS 2 and Gazebo Sim.

---

## 📄 License

This project is intended for educational, research, and development purposes.

