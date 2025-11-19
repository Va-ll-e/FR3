# Franka Research 3 Digital Twin Robot in Unity

This repository documents the steps taken to create a digital twin of the Franka Research 3 (FR3) robot in Unity.

## Prerequisites

- Virtual machine with Ubuntu 24.04 LTS
- Shared folder between the virtual machine and host PC
- ROS2 Jazzy installed on the virtual machine
- Unity with URDF-Importer and ROS-TCP-Connector packages

## Setup Steps

### 1. Install ROS2 and Franka ROS2 Package

On the virtual machine, install ROS2 Jazzy and the Franka ROS2 package following the instructions from the official repository:

- [Franka ROS2](https://github.com/frankarobotics/franka_ros2)

### 2. Generate URDF File

Generate the URDF file for the FR3 robot using the Franka Description package:

- [Franka Description](https://github.com/frankarobotics/franka_description)

Alternatively, the URDF file is included in the `Assets` folder of this repository.

### 3. Install Unity Packages

Install the following Unity packages:

- [URDF-Importer](https://github.com/Unity-Technologies/URDF-Importer)
- [ROS-TCP-Connector](https://github.com/Unity-Technologies/ROS-TCP-Connector)

### 4. Import URDF into Unity

Import the URDF file into your Unity project to create the robot model.

### 5. Configure the Robot

Apply the following tweaks to the imported robot:

- Set the base link as immovable.
- Set links link1 to link7 to Drive type "Target" instead of "Force".

### 6. Set Up ROS-TCP-Endpoint Server

On the virtual machine, build the ROS-TCP-Endpoint package:

- [ROS-TCP-Endpoint](https://github.com/Unity-Technologies/ROS-TCP-Endpoint) (use the `main-ros2` branch)

Run the default server endpoint with:

```
ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:=192.xxx.xxx.xxx
```

Replace `192.xxx.xxx.xxx` with the appropriate IP address.

### 7. Create Subscription Script

Create a script in Unity that subscribes to the `JointState` topic. Ensure that the ROS-TCP-Connector recognizes it, and set the protocol to ROS2 in the settings (it defaults to ROS1).
